---
merged_at: 2026-01-26T23:04:06.001975
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-production-upgrade-strategies -->

# AKS production upgrade strategies

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade your production Azure Kubernetes Service (AKS) clusters safely by using these proven patterns. Each strategy is optimized for specific business constraints and risk tolerance.

## What this article covers

This article provides tested upgrade patterns for production AKS clusters and focuses on:

- Blue-green deployments for zero-downtime upgrades.
- Staged fleet upgrades across multiple environments.
- Safe Kubernetes version adoption with validation gates.
- Emergency security patching for rapid common vulnerabilities and exposures (CVE) response.
- Application resilience patterns for seamless upgrades.

These patterns are best for production environments, site reliability engineers, and platform teams that require minimal downtime and maximum safety.

For more information, see these related articles:

- To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

## Choose your strategy

| Your priority | Best pattern | Downtime | Time to complete |
|---|---|---|---|
| Zero downtime |
|

[Staged fleet upgrades](#scenario-2-stage-upgrades-across-environments)[Canary with validation](#scenario-3-safe-kubernetes-version-intake)[Automated patching](#scenario-4-fastest-security-patch-deployment)[Resilient architecture](#scenario-5-application-architecture-for-seamless-upgrades)#### Role-based quick start

| Role | Start here |
|---|---|
| Site reliability engineer/Platform |
|

[Stateful workload patterns](stateful-workload-upgrades)[Scenario 5](#scenario-5-application-architecture-for-seamless-upgrades)[Scenario 4](#scenario-4-fastest-security-patch-deployment)## Scenario 1: Minimal downtime production upgrades

**Challenge:** "I need to upgrade my production cluster with less than 2 minutes of downtime during business hours."

**Strategy:** Use blue-green deployment with intelligent traffic shifting.

To learn more, see [Blue-green deployment patterns](/en-us/azure/architecture/guide/aks/blue-green-deployment-for-aks) and [Azure Traffic Manager configuration](/en-us/azure/traffic-manager/traffic-manager-configure-weighted-routing-method).

### Quick implementation (15 minutes)

```
# 1. Create green cluster (parallel to blue)
az aks create --name myaks-green --resource-group myRG \
--kubernetes-version 1.29.0 --enable-cluster-autoscaler \
--min-count 3 --max-count 10
# 2. Deploy application to green cluster
kubectl config use-context myaks-green
kubectl apply -f ./production-manifests/
# 3. Validate green cluster
# Run your application-specific health checks here
# Examples: API endpoint tests, database connectivity, dependency checks
# 4. Switch traffic (<30-second downtime)
az network traffic-manager endpoint update \
--profile-name prod-tm --name green-endpoint --weight 100
az network traffic-manager endpoint update \
--profile-name prod-tm --name blue-endpoint --weight 0
```


** Detailed step-by-step guide**

#### Prerequisites

- Secondary cluster capacity planned.
- Application supports horizontal scaling.
- Database connections use connection pooling.
- Health checks configured (
`/health`

,`/ready`

). - Rollback procedure tested in staging.

#### Step 1: Prepare the blue-green infrastructure

```
# Create resource group for green cluster
az group create --name myRG-green --location eastus2
# Create green cluster with same configuration as blue
az aks create \
--resource-group myRG-green \
--name myaks-green \
--kubernetes-version 1.29.0 \
--node-count 3 \
--enable-cluster-autoscaler \
--min-count 3 \
--max-count 10 \
--enable-addons monitoring \
--generate-ssh-keys
```


#### Step 2: Deploy and validate the green environment

```
# Get green cluster credentials
az aks get-credentials --resource-group myRG-green --name myaks-green
# Deploy application stack
# Apply your Kubernetes manifests in order:
kubectl apply -f ./your-manifests/namespace.yaml # Create namespace
kubectl apply -f ./your-manifests/secrets/ # Deploy secrets
kubectl apply -f ./your-manifests/configmaps/ # Deploy config maps
kubectl apply -f ./your-manifests/deployments/ # Deploy applications
kubectl apply -f ./your-manifests/services/ # Deploy services
# Wait for all pods to be ready
kubectl wait --for=condition=ready pod --all --timeout=300s
# Validate application health
kubectl get pods -A
kubectl logs -l app=my-app --tail=50
```


#### Step 3: Traffic switching (critical 30-second window)

```
# Pre-switch validation
curl -f https://myapp-green.eastus2.cloudapp.azure.com/health
if [ $? -ne 0 ]; then echo "Green health check failed!"; exit 1; fi
# Execute traffic switch
az network dns record-set cname set-record \
--resource-group myRG-dns \
--zone-name mycompany.com \
--record-set-name api \
--cname myapp-green.eastus2.cloudapp.azure.com
# Immediate validation
sleep 30
curl -f https://api.mycompany.com/health
```


#### Step 4: Monitor and validate

```
# Monitor traffic and errors for 15 minutes
kubectl top nodes
kubectl top pods
kubectl logs -l app=my-app --since=15m | grep ERROR
# Check application metrics
curl https://api.mycompany.com/metrics | grep http_requests_total
```


### Common pitfalls and FAQs

**Expand for quick troubleshooting and tips**

**Domain Name System (DNS) propagation is slow:**Use low time-to-live values before upgrade, and validate the DNS cache flush.**Pods stuck terminating:**Check for finalizers, long shutdown hooks, or pod disruption budgets (PDBs) with`maxUnavailable: 0`

.**Traffic not shifting:**Validate Azure Load Balancer/Azure Traffic Manager configuration and health probes.**Rollback fails:**Always keep the blue cluster ready until the green cluster is fully validated.**Q: Can I use open-source software tools for validation?****A:**Yes. Use[kube-no-trouble](https://github.com/doitintl/kube-no-trouble)for API checks and[Trivy](https://aquasecurity.github.io/trivy/)for image scanning.

**Q: What's unique to AKS?****A:**Native integration with Traffic Manager, Azure Kubernetes Fleet Manager, and node image patching for zero-downtime upgrades.


### Advanced configuration

For applications that require <30-second downtime:

```
# Use session affinity during transition
apiVersion: v1
kind: Service
metadata:
name: my-app
spec:
sessionAffinity: ClientIP
sessionAffinityConfig:
clientIP:
timeoutSeconds: 300
```


### Success validation

To validate your progress, use the following checklist:

- Application responds within two seconds.
- No 5xx errors are in logs.
- Database connections are stable.
- User sessions are preserved.

### Emergency rollback (if needed)

```
# Immediate rollback to blue cluster
az network dns record-set cname set-record \
--resource-group myRG-dns \
--zone-name mycompany.com \
--record-set-name api \
--cname myapp-blue.eastus2.cloudapp.azure.com
```


**Expected outcome:** Less than 2-minute total downtime, zero data loss, and full rollback capability.

```
az aks create \
--resource-group production-rg \
--name aks-green-cluster \
--kubernetes-version 1.29.0 \
--node-count 3 \
--tier premium \
--auto-upgrade-channel patch \
--planned-maintenance-config ./maintenance-window.json
```


## Verify cluster readiness

```
az aks get-credentials --resource-group production-rg --name aks-green-cluster
kubectl get nodes
```


### Implementation steps

#### Step 1: Deploy the application to a green cluster

```
# Deploy application stack
kubectl apply -f ./k8s-manifests/
kubectl apply -f ./monitoring/
# Wait for all pods to be ready
kubectl wait --for=condition=ready pod --all --timeout=300s
# Validate application health
curl -f http://green-cluster-ingress/health
```


#### Step 2: Run traffic shift

```
# Update DNS or load balancer to point to green cluster
az network dns record-set a update \
--resource-group dns-rg \
--zone-name contoso.com \
--name api \
--set aRecords[0].ipv4Address="<green-cluster-ip>"
# Monitor traffic shift (should complete in 60-120 seconds)
watch kubectl top pods -n production
```


#### Step 3: Validate and clean up

```
# Verify zero errors in application logs
kubectl logs -l app=api --tail=100 | grep -i error
# Monitor key metrics for 15 minutes
kubectl get events --sort-by='.lastTimestamp' | head -20
# After validation, decommission blue cluster
az aks delete --resource-group production-rg --name aks-blue-cluster --yes
```


### Success metrics

**Downtime:**<2 minutes (DNS propagation time)**Error rate:**0% during transition**Recovery time:**<5 minutes if rollback needed

## Scenario 2: Stage upgrades across environments

**Challenge:** "I need to safely test upgrades through dev/test/production with proper validation gates."

**Strategy:** Use Azure Kubernetes Fleet Manager with staged rollouts.

To learn more, see the [Azure Kubernetes Fleet Manager overview](/en-us/azure/kubernetes-fleet/overview) and [Update orchestration](/en-us/azure/kubernetes-fleet/update-orchestration).

### Prerequisites

```
# Install Fleet extension
az extension add --name fleet
az extension update --name fleet
# Create Fleet resource
az fleet create \
--resource-group fleet-rg \
--name production-fleet \
--location eastus
```


### Implementation steps

#### Step 1: Define stage configuration

Create `upgrade-stages.json`

:

```
{
"stages": [
{
"name": "development",
"groups": [{ "name": "dev-clusters" }],
"afterStageWaitInSeconds": 1800
},
{
"name": "testing",
"groups": [{ "name": "test-clusters" }],
"afterStageWaitInSeconds": 3600
},
{
"name": "production",
"groups": [{ "name": "prod-clusters" }],
"afterStageWaitInSeconds": 0
}
]
}
```


#### Step 2: Add clusters to a fleet

```
# Add development clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name dev-east \
--member-cluster-id "/subscriptions/.../clusters/aks-dev-east" \
--group dev-clusters
# Add test clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name test-east \
--member-cluster-id "/subscriptions/.../clusters/aks-test-east" \
--group test-clusters
# Add production clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name prod-east \
--member-cluster-id "/subscriptions/.../clusters/aks-prod-east" \
--group prod-clusters
```


#### Step 3: Create and run a staged update

```
# Create staged update run
az fleet updaterun create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name k8s-1-29-upgrade \
--upgrade-type Full \
--kubernetes-version 1.29.0 \
--node-image-selection Latest \
--stages upgrade-stages.json
# Start the staged rollout
az fleet updaterun start \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name k8s-1-29-upgrade
```


#### Step 4: Validation gates between stages

After dev stage (30-minute soak):

```
# Run automated test suite
./scripts/run-e2e-tests.sh dev-cluster
./scripts/performance-baseline.sh dev-cluster
# Check for any regressions
kubectl get events --sort-by='.lastTimestamp' | grep -i warn
```


After test stage (60-minute soak):

```
# Extended testing with production-like load
./scripts/load-test.sh test-cluster 1000-users 15-minutes
./scripts/chaos-engineering.sh test-cluster
# Manual approval gate
echo "Approve production deployment? (y/n)"
read approval
```


### Common pitfalls and FAQs

**Expand for quick troubleshooting and tips**

**Stage fails because of quota:**Precheck regional quotas for all clusters in the fleet.**Validation scripts fail:**Ensure that test scripts are idempotent and have clear pass/fail output.**Manual approval delays:**Use automation for nonproduction. Require manual only for production.**Q: Can I use open-source software tools for validation?****A:**Yes. Integrate[Sonobuoy](https://sonobuoy.io/)for conformance and[kube-bench](https://github.com/aquasecurity/kube-bench)for security.

**Q: What's unique to AKS?****A:**Azure Kubernetes Fleet Manager enables true staged rollouts and validation gates natively.


## Scenario 3: Safe Kubernetes version intake

**Challenge:** "I need to adopt Kubernetes 1.30 without breaking existing workloads or APIs."

**Strategy:** Use multiphase validation with canary deployment.

To learn more, see [Canary deployments](/en-us/azure/architecture/reference-architectures/containers/aks-microservices/aks-microservices-advanced#deployment-strategies) and [API deprecation policies](https://kubernetes.io/docs/reference/using-api/deprecation-policy/).

### Implementation steps

#### Step 1: API deprecation analysis

```
# Install and run API deprecation scanner
kubectl apply -f https://github.com/doitintl/kube-no-trouble/releases/latest/download/knt-full.yaml
# Scan for deprecated APIs
kubectl run knt --image=doitintl/knt:latest --rm -it --restart=Never -- \
-c /kubeconfig -o json > api-deprecation-report.json
# Review and remediate findings
cat api-deprecation-report.json | jq '.[] | select(.deprecated==true)'
```


To learn more, see the [Kubernetes API deprecation guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/) and [kube-no-trouble documentation](https://github.com/doitintl/kube-no-trouble).

#### Step 2: Create a canary environment

```
# Create canary cluster with target version
az aks create \
--resource-group canary-rg \
--name aks-canary-k8s130 \
--kubernetes-version 1.30.0 \
--node-count 2 \
--tier premium \
--enable-addons monitoring
# Deploy subset of workloads
kubectl apply -f ./canary-manifests/
```


#### Step 3: Progressive workload migration

```
# Phase 1: Stateless services (20% traffic)
kubectl patch service api-service -p '{"spec":{"selector":{"version":"canary"}}}'
./scripts/monitor-error-rate.sh 15-minutes
# Phase 2: Background jobs (50% traffic)
kubectl scale deployment batch-processor --replicas=3
./scripts/validate-job-completion.sh
# Phase 3: Critical services (100% traffic)
kubectl patch deployment critical-api -p '{"spec":{"template":{"metadata":{"labels":{"cluster":"canary"}}}}}'
```


#### Step 4: Feature gate validation

```
# Test new Kubernetes 1.30 features
apiVersion: v1
kind: ConfigMap
metadata:
name: feature-validation
data:
test-script: |
# Test new security features
kubectl auth can-i create pods --as=service-account:default:test-sa
# Validate performance improvements
kubectl top nodes --use-protocol-buffers=true
# Check new API versions
kubectl api-versions | grep "v1.30"
```


### Success metrics

**API compatibility:**100% (zero breaking changes)**Performance:**≤5% regression in key metrics**Feature adoption:**New features validated in canary

## Scenario 4: Fastest security patch deployment

**Challenge:** "A critical CVE was announced. I need patches deployed across all clusters within 4 hours."

**Strategy:** Use automated node image patching with minimal disruption.

To learn more, see [Node image upgrade strategies](node-image-upgrade), [Auto-upgrade channels](auto-upgrade-cluster), and [Security patching best practices](/en-us/azure/aks/operator-best-practices-cluster-security).

### Implementation steps

#### Step 1: Emergency response preparation

```
# Set up automated monitoring for security updates
az aks nodepool update \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--auto-upgrade-channel SecurityPatch
# Configure maintenance window for emergency patches
az aks maintenance-configuration create \
--resource-group production-rg \
--cluster-name aks-prod \
--config-name emergency-security \
--week-index First,Second,Third,Fourth \
--day-of-week Monday,Tuesday,Wednesday,Thursday,Friday \
--start-hour 0 \
--duration 4
```


To learn more, see [Planned maintenance configuration](planned-maintenance) and [Autoupgrade channels](auto-upgrade-cluster#cluster-autoupgrade-channels).

#### Step 2: Automated security scanning

```
# security-scan-cronjob.yaml
apiVersion: batch/v1
kind: CronJob
metadata:
name: security-scanner
spec:
schedule: "0 */6 * * *" # Every 6 hours
jobTemplate:
spec:
template:
spec:
containers:
- name: scanner
image: aquasec/trivy:latest
command:
- trivy
- k8s
- --report
- summary
- cluster
```


#### Step 3: Rapid patch deployment

```
# Trigger immediate node image upgrade for security patches
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--node-image-only \
--max-surge 50% \
--drain-timeout 5
# Monitor patch deployment
watch az aks nodepool show \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--query "upgradeSettings"
```


#### Step 4: Compliance validation

```
# Verify patch installation
kubectl get nodes -o wide
kubectl describe node | grep "Kernel Version"
# Generate compliance report
./scripts/generate-security-report.sh > security-compliance-$(date +%Y%m%d).json
# Notify security team
curl -X POST "$SLACK_WEBHOOK" -d "{\"text\":\"Security patches deployed to production cluster. Compliance report attached.\"}"
```


### Success metrics

**Deployment time:**<4 hours from common vulnerabilities and exposures announcement**Coverage:**100% of nodes patched**Downtime:**<5 minutes per node pool

## Scenario 5: Application architecture for seamless upgrades

**Challenge:** "I want my applications to handle cluster upgrades gracefully without affecting users."

**Strategy:** Use resilient application patterns with graceful degradation.

To learn more, see [Application reliability patterns](/en-us/azure/architecture/framework/resiliency/reliability-patterns), [Pod disruption budgets](https://kubernetes.io/docs/tasks/run-application/configure-pdb/), and [Health check best practices](/en-us/azure/architecture/patterns/health-endpoint-monitoring).

### Implementation steps

#### Step 1: Implement robust health checks

```
# robust-health-checks.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
name: resilient-api
spec:
replicas: 3
template:
spec:
containers:
- name: api
image: myapp:latest
readinessProbe:
httpGet:
path: /health/ready
port: 8080
initialDelaySeconds: 10
periodSeconds: 5
timeoutSeconds: 3
successThreshold: 1
failureThreshold: 3
livenessProbe:
httpGet:
path: /health/live
port: 8080
initialDelaySeconds: 30
periodSeconds: 10
timeoutSeconds: 5
failureThreshold: 3
lifecycle:
preStop:
exec:
command: ["/bin/sh", "-c", "sleep 15"]
```


#### Step 2: Configure pod disruption budgets

```
# optimal-pdb.yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: api-pdb
spec:
selector:
matchLabels:
app: api
maxUnavailable: 1
# Ensures at least 2 pods remain available during upgrades
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: database-pdb
spec:
selector:
matchLabels:
app: database
minAvailable: 2
# Critical: Always keep majority of database pods running
```


#### Step 3: Implement a circuit breaker pattern

```
// circuit-breaker.js
const CircuitBreaker = require('opossum');
const options = {
timeout: 3000,
errorThresholdPercentage: 50,
resetTimeout: 30000,
fallback: () => 'Service temporarily unavailable'
};
const breaker = new CircuitBreaker(callExternalService, options);
// Monitor circuit breaker state during upgrades
breaker.on('open', () => console.log('Circuit breaker opened'));
breaker.on('halfOpen', () => console.log('Circuit breaker half-open'));
```


To learn more, see [Circuit breaker pattern](/en-us/azure/architecture/patterns/circuit-breaker), [Retry pattern](/en-us/azure/architecture/patterns/retry), and [Application resilience](/en-us/azure/well-architected/reliability/).

#### Step 4: Database connection resilience

```
# connection-pool-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
name: db-config
data:
database.yml: |
production:
adapter: postgresql
pool: 25
timeout: 5000
retry_attempts: 3
retry_delay: 1000
connection_validation: true
validation_query: "SELECT 1"
test_on_borrow: true
```


### Success metrics

**Error rate:**<0.01% during upgrades**Response time:**<10% degradation**Recovery time:**<30 seconds after node replacement

## Monitoring and alerting setup

To learn more, see the [AKS monitoring overview](monitor-aks), [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview), and [Prometheus metrics](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).

### Essential metrics to monitor

```
# upgrade-monitoring.yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
name: upgrade-monitoring
spec:
groups:
- name: upgrade.rules
rules:
- alert: UpgradeInProgress
expr: kube_node_spec_unschedulable > 0
for: 1m
annotations:
summary: "Node upgrade in progress"
- alert: HighErrorRate
expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.01
for: 2m
annotations:
summary: "High error rate during upgrade"
- alert: PodEvictionFailed
expr: increase(kube_pod_container_status_restarts_total[5m]) > 5
for: 1m
annotations:
summary: "Multiple pod restarts detected"
```


### Dashboard configuration

```
{
"dashboard": {
"title": "AKS Upgrade Dashboard",
"panels": [
{
"title": "Upgrade Progress",
"targets":
[
"kube_node_info",
"kube_node_status_condition"
]
},
{
"title": "Application Health",
"targets":
[
"up{job='kubernetes-pods'}",
"http_request_duration_seconds"
]
}
]
}
}
```


## Troubleshooting guide

To learn more, see the [AKS troubleshooting guide](/en-us/azure/aks/troubleshooting), [Node and pod troubleshooting](node-access), and [Upgrade error messages](upgrade-aks-cluster#troubleshoot-aks-cluster-upgrade-error-messages).

### Common issues and solutions

| Issue | Symptoms | Solution |
|---|---|---|
| Stuck node drain | Pods won't evict. | Check PDB configuration, increase drain timeout. |
| High error rates | 5xx responses are increasing. | Verify health checks, check resource limits. |
| Slow upgrades | Takes >2 hours. | Increase `maxSurge` , optimize container startup. |
| DNS resolution | Service discovery is failing. | Verify `CoreDNS` pods, check service endpoints. |

### Emergency rollback procedures

```
# Quick rollback script
#!/bin/bash
echo "Initiating emergency rollback..."
# Switch traffic back to previous cluster
az network traffic-manager endpoint update \
--resource-group traffic-rg \
--profile-name production-tm \
--name current-endpoint \
--target-resource-id "/subscriptions/.../clusters/aks-previous"
# Verify rollback success
curl -f https://api.production.com/health
echo "Rollback completed in $(date)"
```


## Related resources

### Specialized scenarios

[Stateful workloads](stateful-workload-upgrades): Use PostgreSQL, Redis, and MongoDB upgrade patterns.[Upgrade scenarios hub](upgrade-scenarios-hub): Choose your upgrade path.[Basic AKS upgrades](upgrade-aks-cluster): Find simple cluster version upgrades.

### Supporting tools

[Auto-upgrade configuration](auto-upgrade-cluster): Use automated upgrade channels.[Maintenance windows](planned-maintenance): Schedule upgrade windows.[Upgrade monitoring](aks-communication-manager): Use real-time upgrade alerts.

### Best practices

[Cluster reliability](best-practices-app-cluster-reliability): Design for upgrades.[Security guidelines](operator-best-practices-cluster-security): Use secure upgrade practices.[Support policies](support-policies): Understand upgrade support windows.

## Next tasks

**Set up monitoring:**Configure[upgrade notifications](aks-communication-manager)before your first upgrade.**Practice safely:**Test scenarios in staging by using[cluster snapshots](node-pool-snapshot).**Automate gradually:**Start with[auto-upgrade channels](auto-upgrade-cluster)for nonproduction.**Handle stateful data:**Review[stateful workload patterns](stateful-workload-upgrades)if you run databases.

## Related content

- For more help, see
[AKS support options](aks-support-help)or review[common upgrade scenarios](upgrade-cluster#common-upgrade-scenarios-and-recommendations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-gateway-api -->

# Configure Istio ingress with the Kubernetes Gateway API for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

The Istio service mesh add-on supports both [Istio's own ingress traffic management API](istio-deploy-ingress) and the Kubernetes Gateway API for ingress traffic management. You can use the Istio Gateway API [automated deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment) or the [manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). This article describes how to configure ingress traffic management for the Istio service mesh add-on using the Kubernetes Gateway API with the [automated deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment).

## Limitations and considerations

- Using the Kubernetes Gateway API for
[egress traffic management](istio-deploy-egress)with the Istio service mesh add-on is only supported for the[manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). - ConfigMap customizations for
`Gateway`

resources must fall within the Resource customization allow list. Fields not on the allow list are disallowed and blocked via add-on managed webhooks. For more information, see the[Istio service mesh add-on support policy](istio-support-policy#allowed-supported-and-blocked-customizations).

## Prerequisites

- Enable the
[Managed Gateway API](managed-gateway-api)on your AKS cluster. - Install the Istio service mesh add-on revision
`asm-1-26`

or higher. Follow the[installation guide](istio-deploy-addon)if you don't have the Istio service mesh add-on installed yet, or the[upgrade guide](istio-upgrade)if you're on a lower minor revision.

## Set environment variables

Set the following environment variables to use throughout this article:

| Variable | Description |
|---|---|
`RESOURCE_GROUP` |
The name of the resource group containing your AKS cluster. |
`CLUSTER_NAME` |
The name of your AKS cluster. |
`LOCATION` |
The Azure region where your AKS cluster is deployed. |
`KEY_VAULT_NAME` |
The name of the Azure Key Vault resource to be created for storing TLS secrets. If you have an existing resource, use that name. |

## Deploy sample application

Deploy the sample

`httpbin`

application in the`default`

namespace using thecommand.`kubectl apply`

`kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.26/samples/httpbin/httpbin.yaml`


## Create Kubernetes Gateway and HTTPRoute

The example manifest creates an external ingress load balancer service that's accessible from outside the cluster. You can add [annotations](#annotation-customizations) to create an internal load balancer and customize other load balancer settings.

Deploy a Gateway API configuration in the

`default`

namespace with the`gatewayClassName`

set to`istio`

and an`HTTPRoute`

that routes traffic to the`httpbin`

service using the following manifest:`kubectl apply -f - <<EOF apiVersion: gateway.networking.k8s.io/v1 kind: Gateway metadata: name: httpbin-gateway spec: gatewayClassName: istio listeners: - name: http port: 80 protocol: HTTP allowedRoutes: namespaces: from: Same --- apiVersion: gateway.networking.k8s.io/v1 kind: HTTPRoute metadata: name: http namespace: default spec: parentRefs: - name: httpbin-gateway hostnames: ["httpbin.example.com"] rules: - matches: - path: type: PathPrefix value: /get backendRefs: - name: httpbin port: 8000 EOF`

Note

If you're performing a

[minor revision upgrade](istio-upgrade)and have two Istio service mesh add-on revisions installed on your cluster simultaneously, the control plane for the higher minor revision takes ownership of the`Gateways`

by default. You can add the`istio.io/rev`

label to the`Gateway`

to control which control plane revision owns it. If you add the revision label, make sure that you update it accordingly to the appropriate control plane revision before rolling back or completing the upgrade operation.

## Verify resource creation

Verify the

`Deployment`

,`Service`

,`HorizontalPodAutoscaler`

, and`PodDisruptionBudget`

resources were created using the following`kubectl get`

commands:`kubectl get deployment httpbin-gateway-istio kubectl get service httpbin-gateway-istio kubectl get hpa httpbin-gateway-istio kubectl get pdb httpbin-gateway-istio`

Example output:

`# Deployment resource NAME READY UP-TO-DATE AVAILABLE AGE httpbin-gateway-istio 2/2 2 2 31m # Service resource NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE httpbin-gateway-istio LoadBalancer 10.0.65.45 <external-ip> 15021:32053/TCP,80:31587/TCP 33m # HPA resource NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 2 5 3 34m # PDB resource NAME MIN AVAILABLE MAX UNAVAILABLE ALLOWED DISRUPTIONS AGE httpbin-gateway-istio 1 N/A 2 36m`


## Send request to sample application

Try sending a

`curl`

request to the`httpbin`

application. First, set the`INGRESS_HOST`

environment variable:`kubectl wait --for=condition=programmed gateways.gateway.networking.k8s.io httpbin-gateway export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -ojsonpath='{.status.addresses[0].value}')`

Try sending an HTTP request to

`httpbin`

.`curl -s -I -HHost:httpbin.example.com "http://$INGRESS_HOST/get"`

In the output, you should see an

`HTTP 200`

response.

## Secure Istio ingress traffic with the Kubernetes Gateway API

The Istio service mesh add-on supports syncing secrets from Azure Key Vault for securing Gateway API-based ingress traffic with [Transport Layer Security (TLS) termination](https://istio.io/latest/docs/tasks/traffic-management/ingress/secure-ingress/) or [Server Name Indication (SNI) passthrough](https://istio.io/latest/docs/tasks/traffic-management/ingress/ingress-sni-passthrough/). In the following sections, you sync secrets from Azure Key Vault onto your AKS cluster using the [Azure Key Vault provider for Secrets Store Container Storage Interface (CSI) Driver add-on](csi-secrets-store-driver) and terminate TLS at the ingress gateway.

## Create client/server certificates and keys

Create a root certificate and private key for signing the certificates for sample services:

`mkdir httpbin_certs openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj '/O=example Inc./CN=example.com' -keyout httpbin_certs/example.com.key -out httpbin_certs/example.com.crt`

Generate a certificate and a private key for

`httpbin.example.com`

:`openssl req -out httpbin_certs/httpbin.example.com.csr -newkey rsa:2048 -nodes -keyout httpbin_certs/httpbin.example.com.key -subj "/CN=httpbin.example.com/O=httpbin organization" openssl x509 -req -sha256 -days 365 -CA httpbin_certs/example.com.crt -CAkey httpbin_certs/example.com.key -set_serial 0 -in httpbin_certs/httpbin.example.com.csr -out httpbin_certs/httpbin.example.com.crt`


## Set up Azure Key Vault and create secrets

Create an Azure Key Vault instance to supply the certificate and key inputs to the Istio service mesh add-on using the

command. If you already have an Azure Key Vault instance, you can skip this step.`az keyvault create`

`az keyvault create --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --location $LOCATION`

Enable the

[Azure Key Vault provider for Secrets Store (CSI) Driver add-on](csi-secrets-store-driver)on your cluster using thecommand.`az aks enable-addons`

`az aks enable-addons --addons azure-keyvault-secrets-provider --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

If your key vault uses Azure role-based access control (RBAC) for the permissions model, follow the instructions in

[Provide access to Azure Key Vault keys, certificates, and secrets with Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide)to assign an Azure role of*Key Vault Secrets User*for the add-on's user-assigned managed identity. Alternatively, if your key vault uses the vault access policy permissions model, authorize the user-assigned managed identity of the add-on to access Azure Key Vault resource using access policy using thecommand.`az keyvault set-policy`

`OBJECT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.objectId' -o tsv | tr -d '\r') CLIENT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.clientId') TENANT_ID=$(az keyvault show --resource-group $RESOURCE_GROUP --name $KEY_VAULT_NAME --query 'properties.tenantId') az keyvault set-policy --name $KEY_VAULT_NAME --object-id $OBJECT_ID --secret-permissions get list`

Create secrets in Azure Key Vault using the certificates and keys using the following

commands:`az keyvault secret set`

`az keyvault secret set --vault-name $KEY_VAULT_NAME --name test-httpbin-key --file httpbin_certs/httpbin.example.com.key az keyvault secret set --vault-name $KEY_VAULT_NAME --name test-httpbin-crt --file httpbin_certs/httpbin.example.com.crt`


## Deploy SecretProviderClass and sample pod

Deploy the SecretProviderClass to provide Azure Key Vault specific parameters to the CSI driver using the following manifest. In this example,

`test-httpbin-key`

and`test-httpbin-crt`

are the names of the secret objects in Azure Key Vault.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: httpbin-credential-spc spec: provider: azure secretObjects: - secretName: httpbin-credential type: kubernetes.io/tls data: - objectName: test-httpbin-key key: tls.key - objectName: test-httpbin-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $KEY_VAULT_NAME cloudName: "" objects: | array: - | objectName: test-httpbin-key objectType: secret objectAlias: "test-httpbin-key" - | objectName: test-httpbin-crt objectType: secret objectAlias: "test-httpbin-crt" tenantId: $TENANT_ID EOF`

Note

Alternatively, to reference a certificate object type directly from Azure Key Vault, use the following manifest to deploy SecretProviderClass. In this example,

`test-httpbin-cert-pxf`

is the name of the certificate object in Azure Key Vault.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: httpbin-credential-spc spec: provider: azure secretObjects: - secretName: httpbin-credential type: kubernetes.io/tls data: - objectName: test-httpbin-key key: tls.key - objectName: test-httpbin-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $KEY_VAULT_NAME cloudName: "" objects: | array: - | objectName: test-httpbin-cert-pfx #certificate object name from keyvault objectType: secret objectAlias: "test-httpbin-key" - | objectName: test-httpbin-cert-pfx #certificate object name from keyvault objectType: cert objectAlias: "test-httpbin-crt" tenantId: $TENANT_ID EOF`

Deploy a sample pod using the following manifest. The Azure Key Vault provider for Secrets Store (CSI) Driver add-on requires a pod to reference the SecretProviderClass resource to ensure secrets sync from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-httpbin spec: containers: - name: busybox image: mcr.microsoft.com/oss/busybox/busybox:1.33.1 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "httpbin-credential-spc" EOF`


## Verify TLS secret creation

Verify the

`httpbin-credential`

secret was created in the`default`

namespace as defined in the SecretProviderClass resource using the`kubectl describe secret`

command.`kubectl describe secret/httpbin-credential`

Example output:

`Name: httpbin-credential Namespace: default Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: kubernetes.io/tls Data ==== tls.crt: 1180 bytes tls.key: 1675 bytes`


## Deploy TLS Gateway

Create a Kubernetes Gateway that references the

`httpbin-credential`

secret under the TLS configuration using the following manifest:`cat <<EOF | kubectl apply -f - apiVersion: gateway.networking.k8s.io/v1 kind: Gateway metadata: name: httpbin-gateway spec: gatewayClassName: istio listeners: - name: https hostname: "httpbin.example.com" port: 443 protocol: HTTPS tls: mode: Terminate certificateRefs: - name: httpbin-credential allowedRoutes: namespaces: from: Selector selector: matchLabels: kubernetes.io/metadata.name: default EOF`

Note

In the gateway definition,

`tls.certificateRefs.name`

must match the`secretName`

in SecretProviderClass resource.Create a corresponding

`HTTPRoute`

to configure ingress traffic routing to the`httpbin`

service over HTTPS using the following manifest:`cat <<EOF | kubectl apply -f - apiVersion: gateway.networking.k8s.io/v1 kind: HTTPRoute metadata: name: httpbin spec: parentRefs: - name: httpbin-gateway hostnames: ["httpbin.example.com"] rules: - matches: - path: type: PathPrefix value: /status - path: type: PathPrefix value: /delay backendRefs: - name: httpbin port: 8000 EOF`

Get the ingress gateway's external IP address and secure port using the following commands:

`kubectl wait --for=condition=programmed gateways.gateway.networking.k8s.io httpbin-gateway export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -o jsonpath='{.status.addresses[0].value}') export SECURE_INGRESS_PORT=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -o jsonpath='{.spec.listeners[?(@.name=="https")].port}')`

Send an HTTPS request to access the

`httpbin`

service:`curl -v -HHost:httpbin.example.com --resolve "httpbin.example.com:$SECURE_INGRESS_PORT:$INGRESS_HOST" \ --cacert httpbin_certs/example.com.crt "https://httpbin.example.com:$SECURE_INGRESS_PORT/status/418"`

The output should show the

`httpbin`

service return the*418 I’m a Teapot*code.Note

To configure HTTPS ingress access to an HTTPS service, update the TLS mode in the gateway definition to

`Passthrough`

. This configuration instructs the gateway to pass the ingress traffic*as is*, without terminating TLS.

## Annotation customizations

You can add annotations under `spec.infrastructure.annotations`

to [configure load balancer settings](configure-load-balancer-standard#customizations-via-kubernetes-annotations) for the `Gateway`

. For instance, to create an internal load balancer attached to a specific subnet, you can create a `Gateway`

with the following annotations:

```
spec:
# ... existing spec content ...
infrastructure:
annotations:
service.beta.kubernetes.io/azure-load-balancer-internal: "true"
service.beta.kubernetes.io/azure-load-balancer-internal-subnet: "my-subnet"
```


## ConfigMap customizations

The Istio service mesh add-on supports [customizations of the resources](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment) generated for the `Gateways`

, including:

- Service
- Deployment
- Horizontal Pod Autoscaler (HPA)
- Pod Disruption Budget (PDB)

The [default settings for these resources](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#gatewayclass-defaults) are set in the `istio-gateway-class-defaults`

ConfigMap in the `aks-istio-system`

namespace. This ConfigMap must have the `gateway.istio.io/defaults-for-class`

label set to `istio`

for the customizations to take effect for all `Gateways`

with `spec.gatewayClassName: istio`

. The `GatewayClass`

-level ConfigMap is installed by default in the `aks-istio-system`

namespace when the [Managed Gateway API installation](managed-gateway-api) is enabled. It could take up to five minutes for the `istio-gateway-class-defaults`

ConfigMap to get deployed after installing the Managed Gateway API CRDs.

```
kubectl get configmap istio-gateway-class-defaults -n aks-istio-system -o yaml
```


```
...
data:
horizontalPodAutoscaler: |
spec:
minReplicas: 2
maxReplicas: 5
podDisruptionBudget: |
spec:
minAvailable: 1
...
```


You can modify these settings for all Istio `Gateways`

at a `GatewayClass`

level by updating the `istio-gateway-class-defaults`

ConfigMap, or you can set them for individual `Gateway`

resources. For both the `GatewayClass`

-level and `Gateway`

-level `ConfigMaps`

, you must add fields to the allow list for the given resource. If there are customizations both for the `GatewayClass`

and an individual `Gateway`

, the `Gateway`

-level configuration takes precedence.

## Deployment customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
Deployment labels |
`metadata.annotations` |
Deployment annotations |
`spec.replicas` |
Deployment replica count |
`spec.template.metadata.labels` |
Pod labels |
`spec.template.metadata.annotations` |
Pod annotations |
`spec.template.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms` |
Node affinity |
`spec.template.spec.affinity.nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Node affinity |
`spec.template.spec.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution` |
Pod affinity |
`spec.template.spec.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Pod affinity |
`spec.template.spec.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution` |
Pod anti-affinity |
`spec.template.spec.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Pod anti-affinity |
`spec.template.spec.containers.resizePolicy` |
Container resource utilization |
`spec.template.spec.containers.resources.limits` |
Container resource utilization |
`spec.template.spec.containers.resources.requests` |
Container resource utilization |
`spec.template.spec.containers.stdin` |
Container debugging |
`spec.template.spec.containers.stdinOnce` |
Container debugging |
`spec.template.spec.nodeSelector` |
Pod scheduling |
`spec.template.spec.nodeName` |
Pod scheduling |
`spec.template.spec.tolerations` |
Pod scheduling |
`spec.template.spec.topologySpreadConstraints` |
Pod scheduling |

## Service customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
Service labels |
`metadata.annotations` |
Service annotations |
`spec.type` |
Service type |
`spec.loadBalancerSourceRanges` |
Service load balancer settings |
`spec.loadBalancerClass` |
Service load balancer settings |
`spec.externalTrafficPolicy` |
Service traffic policy |
`spec.internalTrafficPolicy` |
Service traffic policy |

## HorizontalPodAutoscaler (HPA) customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
HPA labels |
`metadata.annotations` |
HPA annotations |
`spec.behavior.scaleUp.stabilizationWindowSeconds` |
HPA scale-up behavior |
`spec.behavior.scaleUp.selectPolicy` |
HPA scale-up behavior |
`spec.behavior.scaleUp.policies` |
HPA scale-up behavior |
`spec.behavior.scaleDown.stabilizationWindowSeconds` |
HPA scale-down behavior |
`spec.behavior.scaleDown.selectPolicy` |
HPA scale-down behavior |
`spec.behavior.scaleDown.policies` |
HPA scale-down behavior |
`spec.metrics` |
HPA scaling resource metrics |
`spec.minReplicas` |
HPA minimum replica count. Must not be below 2. |
`spec.maxReplicas` |
HPA maximum replica count |

## PodDisruptionBudget (PDB) customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
PDB labels |
`metadata.annotations` |
PDB annotations |
`spec.minAvailable` |
PDB minimum availability |
`spec.unhealthyPodEvictionPolicy` |
PDB eviction policy |

Note

Modifying the `PDB`

minimum availability and eviction policy can lead to potential errors during cluster/node upgrade and deletion operations. Follow the [PDB troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure) to address *UpgradeFailed* errors due to `PDB`

eviction failures.

## Configure GatewayClass-level settings

Update the

`GatewayClass`

-level ConfigMap in the`aks-istio-system`

namespace using the`kubectl edit configmap`

command:`kubectl edit cm istio-gateway-class-defaults -n aks-istio-system`

Edit the resource settings in the

`data`

section as needed. For example, to update the HPA min/max replicas and add a label to the`Deployment`

, modify the ConfigMap as follows:`... data: deployment: | metadata: labels: test.azureservicemesh.io/deployment-config: "updated" horizontalPodAutoscaler: | spec: minReplicas: 3 maxReplicas: 6 podDisruptionBudget: | spec: minAvailable: 1 ...`

Note

Only one ConfigMap per

`GatewayClass`

is allowed.Now, you should see the

`HPA`

for`httpbin-gateway`

that you created earlier get updated with the new min/max values. Verify the`HPA`

settings using the`kubectl get hpa`

command.`kubectl get hpa httpbin-gateway-istio`

Example output:

`NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 3 6 3 36m`

Verify the

`Deployment`

is updated with the new label using the`kubectl get deployment`

command.`kubectl get deployment httpbin-gateway-istio -ojsonpath='{.metadata.labels.test\.azureservicemesh\.io\/deployment-config}'`

Example output:

`updated`


## Configure settings for a specific gateway

Create a ConfigMap with resource customizations for the

`httpbin`

Gateway using the following manifest:`kubectl apply -f - <<EOF apiVersion: v1 kind: ConfigMap metadata: name: gw-options data: horizontalPodAutoscaler: | spec: minReplicas: 2 maxReplicas: 4 deployment: | metadata: labels: test.azureservicemesh.io/deployment-config: "updated-per-gateway" EOF`

Update the

`httpbin`

`Gateway`

to reference the ConfigMap:`spec: # ... existing spec content ... infrastructure: parametersRef: group: "" kind: ConfigMap name: gw-options`

Apply the update using the

`kubectl apply`

command.`kubectl apply -f httpbin-gateway-updated.yaml`

Verify the

`HPA`

is updated with the new min/max values using the`kubectl get hpa`

command. If you also configured the`GatewayClass`

-level ConfigMap, the`Gateway`

-level settings should take precedence.`kubectl get hpa httpbin-gateway-istio`

Example output:

`NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 2 4 2 4h14m`

Inspect the

`Deployment`

labels to ensure that the`test.azureservicemesh.io/deployment-config`

is updated to the new value using the`kubectl get deployment`

command.`kubectl get deployment httpbin-gateway-istio -ojsonpath='{.metadata.labels.test\.azureservicemesh\.io\/deployment-config}'`

Example output:

`updated-per-gateway`


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring any charges.

Delete the Gateway and HTTPRoute resources using the following

`kubectl delete`

commands:`kubectl delete gateways.gateway.networking.k8s.io httpbin-gateway kubectl delete httproute httpbin`

If you created a ConfigMap to customize your Gateway resources, delete it using the

`kubectl delete configmap`

command.`kubectl delete configmap gw-options`

If you created a SecretProviderClass and secret to use for TLS termination delete the resources using the following

`kubectl delete`

commands:`kubectl delete secret httpbin-credential kubectl delete pod secrets-store-sync-httpbin kubectl delete secretproviderclass httpbin-credential-spc`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-windows-gpu -->

# Use Windows GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Windows and [Linux](gpu-cluster) node pools to run compute-intensive Kubernetes workloads.

This article helps you provision Windows nodes with schedulable GPUs on new and existing AKS clusters (preview).

## Supported GPU-enabled virtual machines (VMs)

To view supported GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- Updating an existing Windows node pool to add GPU isn't supported.
- Not supported on Kubernetes version 1.28 and below.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-windows-container-deploy-cli),[Azure PowerShell](learn/quick-windows-container-deploy-powershell), or the[Azure portal](learn/quick-windows-container-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed and configured to use the
`--gpu-driver`

field with the`az aks nodepool add`

command. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command. The following example command gets the credentials for the`az aks get-credentials`

*myAKSCluster*in the*myResourceGroup*resource group:`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Using Windows GPU with automatic driver installation

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [DirectX device plugin for Kubernetes](https://github.com/aarnaud/k8s-directx-device-plugin), GPU driver installation, and more. When you create a Windows node pool with a supported GPU-enabled VM, these components and the appropriate NVIDIA CUDA or GRID drivers are installed. For NC and ND series VM sizes, the CUDA driver is installed. For NV series VM sizes, the GRID driver is installed.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `WindowsGPUPreview`

feature flag

Register the

`WindowsGPUPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a Windows GPU-enabled node pool (preview)

To create a Windows GPU-enabled node pool, you need to use a supported GPU-enabled VM size and specify the `os-type`

as `Windows`

. The default Windows `os-sku`

is `Windows2022`

, but all Windows `os-sku`

options are supported.

Create a Windows GPU-enabled node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type Windows \ --kubernetes-version 1.29.0 \ --node-vm-size Standard_NC6s_v3`

Check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).Once you confirm that your GPUs are schedulable, you can run your GPU workload.


#### Specify GPU Driver Type (preview)

By default, AKS specifies a default GPU driver type for each supported GPU-enabled VM. Because workload and driver compatibility are important for functioning GPU workloads, you can specify the driver type for your Windows GPU node. This feature is not supported for Linux GPU node pools.

When creating a Windows agent pool with GPU support, you have the option to specify the type of GPU driver using the `--driver-type`

flag.

The available options are:

- GRID: For applications requiring virtualization support.
- CUDA: Optimized for computational tasks in scientific computing and data-intensive applications.

Note

When you set the `--driver-type`

flag, you assume responsibility for ensuring that the selected driver type is compatible with the specific VM size and configuration of your node pool. While AKS attempts to validate compatibility, there are scenarios where the node pool creation might fail due to incompatibilities between the specified driver type and the underlying VM or hardware.

To create a Windows GPU-enabled node pool with a specific GPU Driver type, use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--os-type Windows \
--kubernetes-version 1.29.0 \
--node-vm-size Standard_NC6s_v3 \
--driver-type GRID
```


For example, the above command creates a GPU-enabled node pool using the `GRID`

GPU driver type. Selecting this driver type overrides the default of `CUDA`

driver type for NC series VM skus.

## Using Windows GPU with manual driver installation

When creating a Windows node pool with N-series (NVIDIA GPU) VM sizes in AKS, the GPU driver and Kubernetes DirectX device plugin are installed automatically. To bypass this automatic installation, use the following steps:

[Skip GPU driver installation](#skip-gpu-driver-installation)by setting the configuration`--gpu-driver none`

at node pool create time.[Manual installation of the Kubernetes DirectX device plugin](#manually-install-the-kubernetes-directx-device-plugin).

### Skip GPU driver installation

AKS has automatic GPU driver installation enabled by default. In some cases, such as installing your own drivers, you may want to skip GPU driver installation.

Note

The `gpu-driver`

API field is a suggested alternative for customers previously using the `--skip-gpu-driver-install`

node pool tag.

- The
`--skip-gpu-driver-install`

node pool tag on AKS will be retired on 14 August 2025. To retain the existing behavior of skipping automatic GPU driver installation, upgrade your node pools to the latest node image version and set the`--gpu-driver`

field to`none`

. After 14 August 2025, you won't be able to provision AKS GPU-enabled node pools with the`--skip-gpu-driver-install`

node pool tag to bypass this default behavior. For more information, see.`skip-gpu-driver`

tag retirement

Create a node pool using the

command and setting the API field`az aks nodepool add`

`--gpu-driver`

to`none`

to skip automatic GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022 \ --gpu-driver none`


Note

If the `--node-vm-size`

that you're using isn't yet onboarded on AKS, you can't use GPUs and the `--gpu-driver`

field doesn't work.

### Manually install the Kubernetes DirectX device plugin

You can deploy a DaemonSet for the Kubernetes DirectX device plugin, which runs a pod on each node to provide the required drivers for the GPUs.

Add a node pool to your cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022`


## Create a namespace and deploy the Kubernetes DirectX device plugin

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*k8s-directx-device-plugin.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler # reserves resources for critical add-on pods so that they can be rescheduled after # a failure. This annotation works in tandem with the toleration below. annotations: scheduler.alpha.kubernetes.io/critical-pod: "" labels: name: nvidia-device-plugin-ds spec: tolerations: # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode. # This, along with the annotation above marks this pod as a critical add-on. - key: CriticalAddonsOnly operator: Exists - key: nvidia.com/gpu operator: Exists effect: NoSchedule - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" containers: - image: mcr.microsoft.com/aks/aks-windows-gpu-device-plugin:0.0.17 name: nvidia-device-plugin-ctr securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`microsoft.com/directx: 1`

. Your output should look similar to the following condensed example output:`Capacity: [...] microsoft.com.directx/gpu: 1 [...]`


## Clean up resources

Remove the associated Kubernetes objects you created in this article using the

command.`kubectl delete job`

`kubectl delete jobs windows-gpu-workload`


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-node-pools-rolling -->

# Configure rolling upgrades for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A rolling upgrade strategy upgrades nodes one at a time (or a few at a time), minimizing workload disruption while ensuring the node pool remains available throughout the upgrade process. This article explains how to configure rolling upgrades for AKS node pools, including surge settings, drain timeout, and soak time.

## Before you begin

- Ensure your control plane is already upgraded to the target Kubernetes version. You can't upgrade node pools to a version higher than the control plane. For more information, see
[Upgrade the AKS cluster control plane](upgrade-aks-control-plane). - If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - You need the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role permission to configure rolling upgrades for AKS node pools.

## Overview of rolling upgrade behavior

During a rolling upgrade, AKS performs the following operations for each node in the node pool:

**Add surge nodes**: Add new buffer nodes based on max surge (`--max-surge`

) settings to maintain capacity during the upgrade.**Cordon and drain nodes**:[Cordon and drain](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)the old nodes one at a time to minimize disruption to running applications. If you're using max surge, it cordons and drains as many nodes at the same time as the number of buffer nodes specified.**Wait for soak time**(optional): Wait for a configured[soak duration](#set-node-soak-time-value)before proceeding to allow workloads to stabilize on the new nodes before continuing the upgrade.**Reimage old nodes**: When the old nodes are drained, they're reimaged to receive the new version. The reimaged nodes become the buffer nodes for the next set of nodes to be upgraded.**Repeat**: The process repeats until all nodes in the node pool are upgraded.**Remove surge nodes**: After all nodes are upgraded, any remaining buffer nodes are removed, maintaining the original node pool size and balance.

## Configure rolling upgrade settings

### Customize node surge

Important

- Node surges require subscription quota for the requested max surge count for each upgrade operation. For example, a cluster that has five node pools, each with a count of four nodes, has a total of 20 nodes. If each node pool has a max surge value of 50%, extra compute and IP quota of 10 nodes (
*two*nodes ×*five*pools) is required to complete the upgrade. - The max surge setting on a node pool is persistent. Subsequent Kubernetes upgrades or node version upgrades use this setting. You can change the max surge value for your node pools at any time. For production node pools, we recommend a max surge setting of 33%.
- If you're using Azure CNI, validate there are available IPs in the subnet to
[satisfy IP requirements of Azure CNI](configure-azure-cni).

AKS configures upgrades to surge with one extra node by default. A default value of *one* for the max surge setting enables AKS to minimize workload disruption by creating an extra node before the cordon/drain of existing applications to replace an older versioned node. You can customize the max surge value per node pool. When you increase the max surge value, the upgrade process completes faster, but you might experience more disruptions during the upgrade process.

For example, a max surge value of `100%`

provides the fastest possible upgrade process but also causes all nodes in the node pool to be drained simultaneously. You might want to use a higher value like this for testing environments. For production node pools, we recommend a max surge setting of `33%`

.

AKS accepts both integer values and a percentage value for max surge. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five extra nodes to surge |
| Percentage | `50%` |
Surge value of half the current node count in the pool |

Max surge percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count. If the max surge value is higher than the required number of nodes to be upgraded, the number of nodes to be upgraded is used for the max surge value.

#### Set max surge value

Set max surge values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--max-surge`

parameter. For example:```
# Set max surge for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33%
# Update max surge for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 5
```


### Customize unavailable nodes

Important

- You must set max surge to
`0`

in order to set a max unavailable value. The two values can't both be active at the same time. - Max unavailable doesn't create surge nodes during the upgrade process. Instead, AKS cordons
*n*nodes (the max unavailable value) at a time and evicts the pods to other nodes in the agent pool. This might cause workload disruptions if the pods can't be scheduled. - Max unavailable might cause more failures due to unsatisfied Pod Disruption Budgets (PDBs) since there are fewer resources for pods to be scheduled on. For more information, see
[Troubleshooting for Pod Disruption Budgets](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure). - You can't set max unavailable on system node pools.

AKS can also configure upgrades to not use a surge node and upgrade the nodes in place. The max unavailable value determines how many nodes can be simultaneously cordoned and drained from the existing node pool nodes.

AKS accepts both integer values and a percentage value for max unavailable. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five nodes are cordoned from the existing nodes |
| Percentage | `50%` |
Half the current node count in the pool will be unavailable |

Max unavailable percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count.

#### Set max unavailable value

Set max unavailable values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--max-unavailable`

parameter. For example:```
# Set max unavailable for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Update max unavailable for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Set max unavailable at upgrade time
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
```


### Customize node drain timeout

You might have long-running workloads on certain pods that you can't reschedule to another node during runtime. For example, a memory-intensive stateful workload that must finish running. In these cases, you can configure a node drain timeout that AKS respects in the upgrade workflow.

The default node drain timeout value is 30 minutes. Node drain timeout values can be a minimum of 5 minutes and a maximum of 24 hours.

If the drain timeout value elapses and pods are still running, the upgrade operation stops. Any subsequent `PUT`

operation resumes the stopped upgrade.

Tip

For long-running pods, you should also configure the [ terminationGracePeriodSeconds](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) in your pod spec.

#### Set node drain timeout value

Set node drain timeout (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--drain-time-out`

parameter.```
# Set drain timeout for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 100
# Update drain timeout for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 45
```


### Customize node soak time

To enable a waiting period for a specified duration of time between draining a node and proceeding to reimage it and move on to the next node, you can set the soak time. This soak time gives you the opportunity to perform other tasks during the upgrade process, such as checking application health from a monitoring dashboard.

The default node soak time is 0 minutes. Node soak time values can be a minimum of 0 minutes and a maximum of 30 minutes. We recommend keeping soak time as short as reasonably possible. A higher node soak time increases the total upgrade duration and delays discovery of issues.

#### Set node soak time value

Set node soak time (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--node-soak-duration`

flag.```
# Set node soak time for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--node-soak-duration 10
# Update node soak time for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 5
# Set node soak time when upgrading an existing node pool
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 20
```


## View AKS node upgrade events

View upgrade events using the `kubectl get events`

command to monitor the rolling upgrade progress.

```
kubectl get events --field-selector reason=Drain,reason=Surge,reason=Upgrade
```


Example output during an upgrade event:

```
default 2m1s Normal Drain node/aks-nodepool1-12345678-vmss000001 Draining node: [aks-nodepool1-12345678-vmss000001]
default 9m22s Normal Surge node/aks-nodepool1-12345678-vmss000002 Created a surge node [aks-nodepool1-12345678-vmss000002 nodepool1] for agentpool nodepool1
default 1m45s Normal Upgrade node/aks-nodepool1-12345678-vmss000001 Soak duration 5m0s after draining node: aks-nodepool1-12345678-vmss000001
```


## Recommended AKS node pool upgrade settings for production workloads

The following table outlines recommended node pool upgrade settings for production workloads:

| Setting | Recommendation |
|---|---|
Max surge |
Set to 33% for production node pools |
Drain timeout |
Configure based on your longest-running pod's requirements |
Soak time |
Use a short duration (0-5 minutes) unless you need manual verification |
Pod Disruption Budgets |
Configure PDBs for critical workloads to control pod eviction |
Upgrade order |
Upgrade non-production node pools first to validate the new version |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-upgrade-image -->

# Node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, recommended maintenance windows, and examples to get started.

## How do node image updates work for node auto-provisioning nodes?

By default, NAP node pool virtual machines (VMs) are automatically updated when a new image version is available. You can configure an [AKS-managed node operating system (OS) upgrade schedule maintenance window](#node-os-upgrade-maintenance-windows-for-nap) to control when new images are picked up and applied to your NAP nodes, or [use Karpenter Node Disruption Budgets and Pod Disruption Budgets](#karpenter-node-disruption-budgets-and-pod-disruption-budgets-for-nap) to control how and when disruption occurs during upgrades.

Note

NAP forces the latest image version to be picked up if the existing node image version is older than 90 days. This bypasses any existing maintenance window.

## Node OS upgrade maintenance windows for NAP

You can use the [AKS planned maintenance feature](planned-maintenance) with a [node OS auto-upgrade channel](auto-upgrade-node-os-image) to configure a `aksManagedNodeOSUpgradeSchedule`

maintenance window that controls when to perform node OS security patching scheduled by your designated node OS auto-upgrade channel.

### Node OS upgrade maintenance window behavior and considerations

Keep the following information in mind when configuring a node OS upgrade maintenance window for NAP:

- The
`aksManagedNodeOSUpgradeSchedule`

maintenance configuration determines the window during which NAP picks up a new image. This configuration doesn't necessarily determine when existing nodes are disrupted. - The upgrade mechanism and decision criteria are specific to NAP/Karpenter and are evaluated by NAP's drift logic. NAP respects Karpenter Node Disruption Budgets and Pod Disruption Budgets. For more information about drift, see the
[Karpenter drift documentation](https://karpenter.sh/docs/concepts/disruption/#drift). - These NAP upgrade decisions are separate from the cluster
`NodeImage`

and`SecurityPatch`

channels. However, the`aksManagedNodeOSUpgradeSchedule`

maintenance configuration applies them as well. - We recommend using a maintenance window of four hours or more for reliable operation.
- If no maintenance configuration exists, AKS might use a fallback schedule to pick up new images, which can cause images to be picked up at unexpected times. You can avoid unexpected timing of new images and upgrades by defining an explicit
`aksManagedNodeOSUpgradeSchedule`

. - Allow at least 30 minutes between creating or updating a maintenance configuration and the scheduled start time to ensure AKS has time to reconcile the new configuration.

### Recommended schedule pattern for NAP-managed nodes

We recommend the following schedule pattern for NAP-managed nodes:

**Weekly cadence**: Recommended for routine node image roll outs (for example:*Every week on Sunday*).

## Create a node OS maintenance schedule example

The following sections show you how to create a weekly maintenance window for NAP-managed nodes using the Azure CLI and a JSON configuration file and how to update, view, list, and delete the maintenance configuration.

### Create a maintenance configuration

Create a JSON file named

`nodeosMaintenance.json`

with a weekly maintenance window (for example:*Sunday at 01:00 UTC for 4 hours*).`{ "properties": { "maintenanceWindow": { "durationHours": 4, "schedule": { "weekly": { "intervalWeeks": 1, "dayOfWeek": "Sunday" } }, "startDate": "2025-01-01", "startTime": "01:00", "utcOffset": "+00:00" } } }`

Add the maintenance configuration to your cluster using the

command.`az aks maintenanceconfiguration add`

`az aks maintenanceconfiguration add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`


### Update, view, list, or delete a maintenance configuration

You can use the following commands to update, view, list, or delete a maintenance configuration for NAP-managed nodes:

Update a maintenance configuration by modifying the JSON file and then running the

command.`az aks maintenanceconfiguration update`

`az aks maintenanceconfiguration update \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`

View the details of a maintenance configuration using the

command.`az aks maintenanceconfiguration show`

`az aks maintenanceconfiguration show \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`

List all maintenance configurations for your cluster using the

command.`az aks maintenanceconfiguration list`

`az aks maintenanceconfiguration list \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME`

Delete a maintenance configuration using the

command.`az aks maintenanceconfiguration delete`

`az aks maintenanceconfiguration delete \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`


For complete details, examples, and advanced scenarios, see [Use Planned Maintenance to schedule maintenance windows for your AKS cluster](planned-maintenance).

## Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP

For more information on configuring Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP, see the following resources from the official Karpenter documentation:

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/generation-2-vm -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/generation-2-vms -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-image -->

# Autoupgrade node OS images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS provides multiple autoupgrade channels dedicated to timely node-level OS security updates. This channel is different from cluster-level Kubernetes version upgrades and supersedes it.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Interactions between node OS autoupgrade and cluster autoupgrade

Node-level OS security updates are released at a faster rate than Kubernetes patch or minor version updates. The node OS autoupgrade channel grants you flexibility and enables a customized strategy for node-level OS security updates. Then, you can choose a separate plan for cluster-level Kubernetes version [autoupgrades](auto-upgrade-cluster).
It's best to use both cluster-level [autoupgrades](auto-upgrade-cluster) and the node OS autoupgrade channel together. Scheduling can be fine-tuned by applying two separate sets of [maintenance windows](planned-maintenance) - `aksManagedAutoUpgradeSchedule`

for the cluster [autoupgrade](auto-upgrade-cluster) channel and `aksManagedNodeOSUpgradeSchedule`

for the node OS autoupgrade channel.

## Channels for node OS image upgrades

The selected channel determines the timing of upgrades. When making changes to node OS auto-upgrade channels, allow up to 24 hours for the changes to take effect.

Note

- Node OS image auto-upgrade don't affect the cluster's Kubernetes version.
- Starting with API version 2023-06-01, the default for any new AKS cluster is
`NodeImage`

.

### Node OS channel changes that cause a reimage

The following node os channel transitions will trigger reimage on the nodes:

| From | To |
|---|---|
| Unmanaged | None |
| Unspecified | Unmanaged |
| SecurityPatch | Unmanaged |
| NodeImage | Unmanaged |
| None | Unmanaged |

### Available node OS upgrade channels

The following upgrade channels are available. You're allowed to choose one of these options:

| Channel | Description | OS-specific behavior |
|---|---|---|
`None` |
Your nodes don't have security updates applied automatically. This means you're solely responsible for your security updates. | N/A |
`Unmanaged` |
The OS built-in patching infrastructure automatically applies OS updates. Newly allocated machines are initially unpatched. The OS's infrastructure patches them at some point. | Ubuntu and Azure Linux (CPU node pools) apply security patches through unattended upgrade/dnf-automatic roughly once per day around 06:00 UTC. Windows doesn't automatically apply security patches, so this option behaves equivalently to `None` . You need to manage the reboot process using a tool like
`Unmanaged` . |
`SecurityPatch` |
OS security patches, which are AKS-tested, fully managed, and applied with safe deployment practices. AKS regularly updates the node's virtual hard disk (VHD) with patches from the image maintainer labeled "security only." There might be disruptions when the security patches are applied to the nodes. However AKS is limiting disruptions by only reimaging your nodes only when necessary, such as for certain kernel security packages. When the patches are applied, the VHD is updated and existing machines are upgraded to that VHD, honoring maintenance windows and surge settings. If AKS decides that reimaging nodes isn't necessary, it patches nodes live without draining pods and performs no VHD update. This option incurs the extra cost of hosting the VHDs in your node resource group. If you use this channel, Linux
|

`SecurityPatch`

works on kubernetes patch versions that are deprecated, so long as the minor Kubernetes version is still supported. [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)and[Azure Linux with OS Guard on AKS](use-azure-linux-os-guard)do not support`SecurityPatch`

.`NodeImage`

[unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates)are disabled by default. Node image upgrades are supported as long as cluster Kubernetes minor version is still in support. Node images are AKS-tested, fully managed, and applied with safe deployment practices.## What to choose - SecurityPatch Channel or NodeImage Channel?

There are two important considerations for you to choose between `SecurityPatch`

or `NodeImage`

channels.

| Property | NodeImage Channel | SecurityPatch Channel | Recommended Channel |
|---|---|---|---|
`Speed of shipping` |
The typical build, test, release, and rollout timelines for a new VHD can take approximately two weeks following safe deployment practices. Although in the event of CVEs, accelerated rollouts can occur on a case by case basis. The exact timing when a new VHD hits a region can be monitored via
|

`NodeImage`

, even with safe deployment practices. SecurityPatch has the advantage of 'Live-patching' in Linux environments, where patching leads to selective 'reimaging' and doesn't reimage every time a patch gets applied. Re-image if it happens is controlled by maintenance windows.`SecurityPatch`

`Bugfixes`

`NodeImage`

## Set the node OS autoupgrade channel on a new cluster

- Set the node OS autoupgrade channel on a new cluster using the
command with the`az aks create`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX"
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER \
--node-os-upgrade-channel SecurityPatch \
--generate-ssh-keys
```


## Set the node OS autoupgrade channel on an existing cluster

- Set the node os autoupgrade channel on an existing cluster using the
command with the`az aks update`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --node-os-upgrade-channel SecurityPatch
```


Results:

```
{
"autoUpgradeProfile": {
"nodeOsUpgradeChannel": "SecurityPatch"
}
}
```


## Update ownership and schedule

The default cadence means there's no planned maintenance window applied.

| Channel | Updates Ownership | Default cadence |
|---|---|---|
`Unmanaged` |
OS driven security updates. AKS has no control over these updates. | Nightly around 6AM UTC for Ubuntu and Azure Linux. Monthly for Windows. |
`SecurityPatch` |
AKS-tested, fully managed, and applied with safe deployment practices. For more information, see
|

`NodeImage`

[AKS Node Images in Release tracker](release-tracker)Note

While Windows security updates are released on a monthly basis, using the `Unmanaged`

channel won't automatically apply these updates to Windows nodes. If you choose the `Unmanaged`

channel, you need to manage the reboot process for Windows nodes.

## Node channel known limitations

Currently, when you set the

[cluster autoupgrade channel](auto-upgrade-cluster)to`node-image`

, it also automatically sets the node OS autoupgrade channel to`NodeImage`

. You can't change node OS autoupgrade channel value if your cluster autoupgrade channel is`node-image`

. In order to set the node OS autoupgrade channel value, check the[cluster autoupgrade channel](auto-upgrade-cluster)value isn't`node-image`

.The

`SecurityPatch`

channel isn't supported on Windows OS node pools.

Note

Use CLI version 2.61.0 or above for the `SecurityPatch`

channel.

## Node OS planned maintenance windows

Planned maintenance for the node OS autoupgrade starts at your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of four hours or more.

For more information on Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Node OS autoupgrades FAQ

### How can I check the current nodeOsUpgradeChannel value on a cluster?

Run the `az aks show`

command and check the "autoUpgradeProfile" to determine what value the `nodeOsUpgradeChannel`

is set to:

```
az aks show --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --query "autoUpgradeProfile"
```


Results:

```
{
"nodeOsUpgradeChannel": "SecurityPatch"
}
```


### How can I monitor the status of node OS autoupgrades?

To view the status of your node OS auto upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events as mentioned in [Upgrade an AKS cluster](upgrade-cluster). AKS also emits upgrade-related Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I change the node OS autoupgrade channel value if my cluster autoupgrade channel is set to `node-image`

?

No. Currently, when you set the [cluster autoupgrade channel](auto-upgrade-cluster) to `node-image`

, it also automatically sets the node OS autoupgrade channel to `NodeImage`

. You can't change the node OS autoupgrade channel value if your cluster autoupgrade channel is `node-image`

. In order to be able to change the node OS autoupgrade channel values, make sure the [cluster autoupgrade channel](auto-upgrade-cluster) isn't `node-image`

.

### Why is `SecurityPatch`

recommended over `Unmanaged`

channel?

On the `Unmanaged`

channel, AKS has no control over how and when the security updates are delivered. With `SecurityPatch`

, the security updates are fully tested and follow safe deployment practices. `SecurityPatch`

also honors maintenance windows. For more information, see [Increased security and resiliency of Canonical workloads on Azure](https://techcommunity.microsoft.com/t5/linux-and-open-source-blog/increased-security-and-resiliency-of-canonical-workloads-on/ba-p/3970623).

### Does `SecurityPatch`

always lead to a reimage of my nodes?

AKS limits reimages to only when necessary, such as certain kernel packages that may require a reimage to get fully applied. `SecurityPatch`

is designed to minimize disruptions as much as possible. If AKS decides reimaging nodes isn't necessary, it patches nodes live without draining pods and no VHD update is performed in such cases.

### Why does `SecurityPatch`

channel requires to reach `snapshot.ubuntu.com`

endpoint?

With the `SecurityPatch`

channel, the Linux cluster nodes have to download the required security patches and updates from ubuntu snapshot service described in [ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments](https://ubuntu.com/blog/ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments).

### How do I know if a `SecurityPatch`

or `NodeImage`

upgrade is applied on my node?

Run the `kubectl get nodes --show-labels`

command to list the nodes in your cluster and their labels.

Among the returned labels, you should see a line similar to the following output:

```
kubernetes.azure.com/node-image-version=AKSUbuntu-2204gen2containerd-202410.27.0-2024.12.01
```


Here, the base node image version is `AKSUbuntu-2204gen2containerd-202410.27.0`

. If applicable, the security patch version typically follows. In the above example, it's `2024.12.01`

.

The same details also be looked up in the Azure portal under the node label view:

## Next steps

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).
