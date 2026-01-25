---
merged_at: 2026-01-25T15:16:21.141622
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _aks-production-upgrade-strategies_istio-gateway-api.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: aks-production-upgrade-strategies.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-production-upgrade-strategies -->

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

<!-- DOCUMENTO FUSIONADO: istio-gateway-api.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-gateway-api -->

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

<!-- DOCUMENTO FUSIONADO: __node-auto-provisioning-disruption_ssh__node-access__kms-data-encryption-concep_eee3e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _node-auto-provisioning-disruption_ssh.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-disruption.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-disruption -->

# Configure node disruption policies for node auto-provisioning (NAP) nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node disruption policies for Azure Kubernetes Service (AKS) node auto-provisioning (NAP) nodes and details how disruption works to optimize resource utilization and cost efficiency.

NAP optimizes your cluster by:

- Removing or replacing underutilized nodes.
- Consolidating workloads to reduce costs.
- Respecting disruption budgets and maintenance windows.
- Providing manual control when needed.

## Before you begin

- Read the
[Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning)article, which details[how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work). - Read the
[Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning-networking).

## How does node disruption work for NAP nodes?

Karpenter sets a Kubernetes [finalizer](https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/) on each node and node claim it provisions. The finalizer blocks the deletion of the node object, while the Termination Controller taints and drains the node before removing the underlying node claim.

When the workloads on your nodes scale down, NAP uses disruption rules on the node pool specification to decide when and how to remove those nodes and potentially reschedule your workloads for efficiency.

## Node disruption methods

NAP automatically discovers nodes eligible for disruption and spins up replacements when needed. You can trigger disruption through automated methods like *Expiration*, *Consolidation*, and *Drift*, manual methods, or external systems.

## Expiration

Expiration allows you to set a maximum age for your NAP nodes. Nodes are marked as expired and disrupted after reaching the age you specify for the node pool's `spec.disruption.expireAfter`

value.

### Example expiration configuration

The following example shows how to set the expiration time for NAP nodes to 24 hours:

```
spec:
disruption:
expireAfter: 24h # Expire nodes after 24 hours
```


## Consolidation

NAP works to actively reduce cluster cost by identifying when nodes can be removed because they're empty or underutilized, or when nodes can be replaced with lower priced variants. This process is called *Consolidation*. NAP primarily uses Consolidation to delete or replace nodes for optimal pod placement.

NAP performs the following types of consolidation in order to optimize resource utilization:

**Empty node consolidation**: Deletes any empty nodes in parallel.**Multi-node consolidation**: Deletes multiple nodes, possibly launching a single replacement.**Single-node consolidation**: Deletes any single node, possibly launching a replacement.

You can trigger consolidation through the `spec.disruption.consolidationPolicy`

field in the node pool specification using the `WhenEmpty`

, or `WhenEmptyOrUnderUtilized`

settings. You can also set the `consolidateAfter`

field, which is a time-based condition that determines how long NAP waits after discovering a consolidation opportunity before disrupting the node.

### Example consolidation configuration

The following example shows how to configure NAP to consolidate nodes when they're empty, and to wait 30 seconds after discovering a consolidation opportunity before disrupting the node:

```
disruption:
# Describes which types of nodes NAP should consider for consolidation
# `WhenEmptyOrUnderUtilized`: NAP considers all nodes for consolidation and attempts to remove or replace nodes when it discovers that the node is empty or underutilized and could be changed to reduce cost
# `WhenEmpty`: NAP only considers nodes for consolidation that don't contain any workload pods
consolidationPolicy: WhenEmpty
# The amount of time NAP should wait after discovering a consolidation decision
# Currently, you can only set this value when the consolidation policy is `WhenEmpty`
# You can choose to disable consolidation entirely by setting the string value `Never`
consolidateAfter: 30s
```


## Drift

Drift handles changes to the `NodePool`

/`AKSNodeClass`

resources. Values in the `NodeClaimTemplateSpec`

/`AKSNodeClassSpec`

are reflected in the same way that they're set. A `NodeClaim`

is detected as *drifted* if the values in the associated `NodePool`

/`AKSNodeClass`

don't match the values in the `NodeClaim`

. Similar to the upstream `deployment.spec.template`

relationship to pods, Karpenter annotates the associated `NodePool`

/`AKSNodeClass`

with a hash of the `NodeClaimTemplateSpec`

to check for drift. Karpenter removes the `Drifted`

status condition in the following scenarios:

- The
`Drift`

feature gate isn't enabled but the`NodeClaim`

is drifted. - The
`NodeClaim`

isn't drifted, but has the status condition.

Karpenter or the cloud provider interface might discover [special cases](#special-cases-on-drift) triggered by `NodeClaim`

/`Instance`

/`NodePool`

/`AKSNodeClass`

changes.

### Special cases on drift

In special cases, drift can correspond to multiple values and must be handled differently. Drift on resolved fields can create cases where drift occurs without changes to Custom Resource Definitions (CRDs), or where CRD changes don't result in drift.

For example, if a `NodeClaim`

has `node.kubernetes.io/instance-type: Standard_D2s_v3`

, and requirements change from `node.kubernetes.io/instance-type In [Standard_D2s_v3]`

to `node.kubernetes.io/instance-type In [Standard_D2s_v3, Standard_D4s_v3]`

, the `NodeClaim`

isn't drifted because its value is still compatible with the new requirements. Conversely, if a `NodeClaim`

uses a `NodeClaim`

`imageFamily`

, but the `spec.imageFamily`

field changes, Karpenter detects the `NodeClaim`

as *drifted* and rotates the node to meet that specification.

Important

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations. For more information, see [Subnet drift behavior](node-auto-provisioning-networking#subnet-drift-behavior).

For more information, see [Drift Design](https://github.com/aws/karpenter-core/blob/main/designs/drift.md).

## Termination grace period

You can set a termination grace period for NAP nodes using the `spec.template.spec.terminationGracePeriod`

field in the node pool specification. This setting allows you to configure how long Karpenter waits for pods to terminate gracefully. This setting takes precedence over a pod's `terminationGracePeriodSeconds`

and bypasses `PodDisruptionBudgets`

and the `karpenter.sh/do-not-disrupt`

annotation.

### Example termination grace period configuration

The following example shows how to set a termination grace period of 30 seconds for NAP nodes:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
spec:
terminationGracePeriod: 30s
```


## Disruption budgets

You can rate limit Karpenter's disruption by modifying the `spec.disruption.budgets`

field in the node pool specification. If you leave this setting undefined, Karpenter defaults to one budget with `nodes: 10%`

. Budgets consider nodes that are being deleted for any reason, and they only block Karpenter from voluntary disruptions through expiration, drift, emptiness, and consolidation.

When calculating if a budget blocks nodes from disruption, Karpenter counts the total nodes owned by a node pool and then subtracts nodes that are being deleted and nodes that are `NotReady`

. If the budget is configured with a percentage value, such as `20%`

, Karpenter calculates the number of allowed disruptions as `allowed_disruptions = roundup(total * percentage) - total_deleting - total_notready`

. For multiple budgets in a node pool, Karpenter takes the minimum (most restrictive) value of each of the budgets.

### Schedule and duration fields

When using budgets, you can optionally set the `schedule`

and `duration`

fields to create time-based budgets. These fields allow you to define maintenance windows or specific timeframes when disruption limits are stricter.

**Schedule**uses cron job syntax with special macros like`@yearly`

,`@monthly`

,`@weekly`

,`@daily`

,`@hourly`

.**Duration**allows compound durations like`10h5m`

,`30m`

, or`160h`

. Duration and Schedule must be defined together.

#### Schedule and duration examples

##### Maintenance window budget

Prevent disruptions during business hours:

```
budgets:
- nodes: "0"
schedule: "0 9 * * 1-5" # 9 AM Monday-Friday
duration: 8h # For 8 hours
```


##### Weekend-only disruptions

Only allow disruptions on weekends:

```
budgets:
- nodes: "50%"
schedule: "0 0 * * 6" # Saturday midnight
duration: 48h # All weekend
- nodes: "0" # Block all other times
```


##### Gradual rollout budget

Allow increasing disruption rates:

```
budgets:
- nodes: "1"
schedule: "0 2 * * *" # 2 AM daily
duration: 2h
- nodes: "3"
schedule: "0 4 * * *" # 4 AM daily
duration: 4h
```


### Budget configuration examples

The following `NodePool`

specification has three budgets configured:

- The first budget allows 20% of nodes owned by the node pool to be disrupted at once.
- The second budget acts as a ceiling, only allowing five disruptions when there are more than 25 nodes.
- The last budget blocks disruptions during the first 10 minutes of each day.

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
expireAfter: 720h # 30 * 24h = 720h
budgets:
- nodes: "20%" # Allow 20% of nodes to be disrupted
- nodes: "5" # Cap at maximum 5 nodes
- nodes: "0" # Block all disruptions during maintenance window
schedule: "@daily" # Scheduled daily
duration: 10m # Duration of 10 minutes
```


## Manual node disruption

You can manually disrupt NAP nodes using `kubectl`

or by deleting `NodePool`

resources.

### Remove nodes with kubectl

You can manually remove nodes using the `kubectl delete node`

command. You can delete specific nodes, all NAP-managed nodes, or nodes from a specific node pool by using labels, for example:

```
# Delete a specific node
kubectl delete node $NODE_NAME
# Delete all NAP-managed nodes
kubectl delete nodes -l karpenter.sh/nodepool
# Delete nodes from a specific nodepool
kubectl delete nodes -l karpenter.sh/nodepool=$NODEPOOL_NAME
```


### Delete `NodePool`

resources

The `NodePool`

owns `NodeClaims`

through an owner reference. NAP gracefully terminates nodes through cascading deletion when you delete the associated `NodePool`

.

## Control disruption using annotations

You can block or disable disruption for specific pods, nodes, or entire node pools using annotations.

### Pod controls

Block NAP from disrupting certain pods by setting the `karpenter.sh/do-not-disrupt: "true"`

annotation:

```
apiVersion: apps/v1
kind: Deployment
spec:
template:
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


This annotation prevents voluntary disruption for Expiration, Consolidation, and Drift. However, it doesn't prevent disruption from external systems or manual disruption through `kubectl`

or `NodePool`

deletion.

### Node controls

Block NAP from disrupting specific nodes:

```
apiVersion: v1
kind: Node
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


### Node pool controls

Disable disruption for all nodes in a `NodePool`

:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: ssh.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ssh -->

# Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you eventually need to directly access an AKS node. This access could be for maintenance, log collection, or troubleshooting operations.

You access a node through authentication, which methods vary depending on your Node OS and method of connection. You securely authenticate against AKS Linux and Windows nodes through two options discussed in this article. One requires that you have Kubernetes API access, and the other is through the AKS ARM API, which provides direct private IP information. For security reasons, AKS nodes aren't exposed to the internet. Instead, to connect directly to any AKS nodes, you need to use either `kubectl debug`

or the host's private IP address.

## Access nodes using the Kubernetes API

This method requires usage of `kubectl debug`

command.

### Before you begin

This guide shows you how to create a connection to an AKS node and update the SSH key of your AKS cluster. To follow along the steps, you need to use Azure CLI that supports version 2.0.64 or later. Run `az --version`

to check the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Complete these steps if you don't have an SSH key. Create an SSH key depending on your Node OS Image, for [macOS and Linux](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), or [Windows](/en-us/azure/virtual-machines/linux/ssh-from-windows). Make sure you save the key pair in the OpenSSH format, avoid unsupported formats such as `.ppk`

. Next, refer to [Manage SSH configuration](manage-ssh-node-access) to add the key to your cluster.

### Linux and macOS

Linux and macOS users can access their node using `kubectl debug`

or their private IP Address. Windows users should skip to the Windows Server Proxy section for a workaround to SSH via proxy.

#### Connect using kubectl debug

To create an interactive shell connection, use the `kubectl debug`

command to run a privileged container on your node.

To list your nodes, use the

`kubectl get nodes`

command:`kubectl get nodes -o wide`

Sample output:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE aks-nodepool1-37663765-vmss000000 Ready agent 166m v1.25.6 10.224.0.33 <none> Ubuntu 22.04.2 LTS aks-nodepool1-37663765-vmss000001 Ready agent 166m v1.25.6 10.224.0.4 <none> Ubuntu 22.04.2 LTS aksnpwin000000 Ready agent 160m v1.25.6 10.224.0.62 <none> Windows Server 2022 Datacenter`

Use the

`kubectl debug`

command to start a privileged container on your node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

You now have access to the node through a privileged container as a debugging pod.

Note

You can interact with the node session by running

`chroot /host`

from the privileged container.

#### Exit kubectl debug mode

When you're done with your node, enter the `exit`

command to end the interactive shell session. After the interactive container session closes, delete the debugging pod used with `kubectl delete pod`

.

```
kubectl delete pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx
```


### Windows Server proxy connection for SSH

Follow these steps as a workaround to connect with SSH on a Windows Server node.

#### Create a proxy server

At this time, you can't connect to a Windows Server node directly by using `kubectl debug`

. Instead, you need to first connect to another node in the cluster with `kubectl`

, then connect to the Windows Server node from that node using SSH.

To connect to another node in the cluster, use the `kubectl debug`

command. For more information, follow the above steps in the kubectl section. Create an SSH connection to the Windows Server node from another node using the SSH keys provided when you created the AKS cluster and the internal IP address of the Windows Server node.

Important

The following steps for creating the SSH connection to the Windows Server node from another node can only be used if you created your AKS cluster using the Azure CLI with the `--generate-ssh-keys`

parameter. If you want to use your own SSH keys instead, you can use the `az aks update`

to manage SSH keys on an existing AKS cluster. For more information, see [manage SSH node access](manage-ssh-node-access).

Note

If your Linux proxy node is down or unresponsive, use the [Azure Bastion](/en-us/azure/bastion/bastion-overview) method to connect instead.

Use the

`kubectl debug`

command to start a privileged container on your proxy (Linux) node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

Open a new terminal window and use the

`kubectl get pods`

command to get the name of the pod started by`kubectl debug`

.`kubectl get pods`

Sample output:

`NAME READY STATUS RESTARTS AGE node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 1/1 Running 0 21s`

In the sample output,

*node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx*is the name of the pod started by`kubectl debug`

.Use the

`kubectl port-forward`

command to open a connection to the deployed pod:`kubectl port-forward node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 2022:22`

Sample output:

`Forwarding from 127.0.0.1:2022 -> 22 Forwarding from [::1]:2022 -> 22`

The previous example begins forwarding network traffic from port

`2022`

on your development computer to port`22`

on the deployed pod. When using`kubectl port-forward`

to open a connection and forward network traffic, the connection remains open until you stop the`kubectl port-forward`

command.Open a new terminal and run the command

`kubectl get nodes`

to show the internal IP address of the Windows Server node:`kubectl get no -o custom-columns=NAME:metadata.name,'INTERNAL_IP:status.addresses[?(@.type == \"InternalIP\")].address'`

Sample output:

`NAME INTERNAL_IP aks-nodepool1-19409214-vmss000003 10.224.0.8`

In the previous example,

*10.224.0.62*is the internal IP address of the Windows Server node.Create an SSH connection to the Windows Server node using the internal IP address, and connect to port

`22`

through port`2022`

on your development computer. The default username for AKS nodes is*azureuser*. Accept the prompt to continue with the connection. You're then provided with the bash prompt of your Windows Server node:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' azureuser@10.224.0.62`

Sample output:

`The authenticity of host '10.224.0.62 (10.224.0.62)' can't be established. ECDSA key fingerprint is SHA256:1234567890abcdefghijklmnopqrstuvwxyzABCDEFG. Are you sure you want to continue connecting (yes/no)? yes`

Note

If you prefer to use password authentication, include the parameter

`-o PreferredAuthentications=password`

. For example:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' -o PreferredAuthentications=password azureuser@10.224.0.62`


## Use a host process container to access Windows node

Run the following script to create

`hostprocess.yaml`

. In the script, replace`AKSWINDOWSNODENAME`

with the AKS Windows node name.This specification uses the nanoserver base image. The base image doesn't have PowerShell, but because it runs as a host process container (HPC), PowerShell is available in the underlying VM.

`apiVersion: v1 kind: Pod metadata: labels: pod: hpc name: hpc spec: securityContext: windowsOptions: hostProcess: true runAsUserName: "NT AUTHORITY\\SYSTEM" hostNetwork: true containers: - name: hpc image: mcr.microsoft.com/windows/nanoserver:ltsc2022 # Use nanoserver:1809 for WS2019 command: - powershell.exe - -Command - "Start-Sleep 2147483" imagePullPolicy: IfNotPresent nodeSelector: kubernetes.io/os: windows kubernetes.io/hostname: AKSWINDOWSNODENAME tolerations: - effect: NoSchedule key: node.kubernetes.io/unschedulable operator: Exists - effect: NoSchedule key: node.kubernetes.io/network-unavailable operator: Exists - effect: NoExecute key: node.kubernetes.io/unreachable operator: Exists`

Run

`kubectl apply -f hostprocess.yaml`

to deploy the Windows HPC in the specified Windows node.Use

`kubectl exec -it [HPC-POD-NAME] -- powershell`

.You can run any PowerShell commands inside the HPC container to access the Windows node.


Note

You need to switch the root folder to `C:\`

inside the HPC container to access the files in the Windows node.

## SSH using Azure Bastion for Windows

If your Linux proxy node isn't reachable, using Azure Bastion as a proxy is an alternative. This method requires that you set up an Azure Bastion host for the virtual network in which the cluster resides. See [Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview) for more details.

## SSH using private IPs from the AKS API

If you don't have access to the Kubernetes API, you can get access to properties such as `Node IP`

and `Node Name`

through the [AKS agent pool API ](/en-us/rest/api/aks/agent-pools/get#agentpool), (available on stable versions `07-01-2024`

or above) to connect to AKS nodes.

### Create an interactive shell connection to a node using the IP address

For convenience, AKS nodes are exposed on the cluster's virtual network through private IP addresses. However, you need to be in the cluster's virtual network to SSH into the node. If you don't already have an environment configured, you can use [Azure Bastion](/en-us/azure/bastion/bastion-connect-vm-ssh-linux) to establish a proxy from which you can SSH to cluster nodes. Make sure the Azure Bastion is deployed in the same virtual network as the cluster.

Obtain private IPs using the

`az aks machine list`

command, targeting all the VMs in a specific node pool with the`--nodepool-name`

flag.`az aks machine list --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name nodepool1 -o table`

The following example output shows the internal IP addresses of all the nodes in the node pool:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4 aks-nodepool1-33555069-vmss000001 10.224.0.6 IPv4 aks-nodepool1-33555069-vmss000002 10.224.0.4 IPv4`

To target a specific node inside the node pool, use the

`--machine-name`

flag:`az aks machine show --cluster-name myAKScluster --nodepool-name nodepool1 -g myResourceGroup --machine-name aks-nodepool1-33555069-vmss000000 -o table`

The following example output shows the internal IP address of all the specified node:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4`

SSH to the node using the private IP address you obtained in the previous step. This step is applicable for Linux machines only. For Windows machines, see

[Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview).`ssh -i /path/to/private_key.pem azureuser@10.224.0.33`


## Next steps

If you need more troubleshooting data, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes control plane logs](monitor-aks-reference#resource-logs).

To learn about managing your SSH keys, see [Manage SSH configuration](manage-ssh-node-access).


---

<!-- DOCUMENTO FUSIONADO: _node-access__kms-data-encryption-concepts___istio-latency__troubleshooting_inde_db2229.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-access.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-access -->

# Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you eventually need to directly access an AKS node. This access could be for maintenance, log collection, or troubleshooting operations.

You access a node through authentication, which methods vary depending on your Node OS and method of connection. You securely authenticate against AKS Linux and Windows nodes through two options discussed in this article. One requires that you have Kubernetes API access, and the other is through the AKS ARM API, which provides direct private IP information. For security reasons, AKS nodes aren't exposed to the internet. Instead, to connect directly to any AKS nodes, you need to use either `kubectl debug`

or the host's private IP address.

## Access nodes using the Kubernetes API

This method requires usage of `kubectl debug`

command.

### Before you begin

This guide shows you how to create a connection to an AKS node and update the SSH key of your AKS cluster. To follow along the steps, you need to use Azure CLI that supports version 2.0.64 or later. Run `az --version`

to check the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Complete these steps if you don't have an SSH key. Create an SSH key depending on your Node OS Image, for [macOS and Linux](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), or [Windows](/en-us/azure/virtual-machines/linux/ssh-from-windows). Make sure you save the key pair in the OpenSSH format, avoid unsupported formats such as `.ppk`

. Next, refer to [Manage SSH configuration](manage-ssh-node-access) to add the key to your cluster.

### Linux and macOS

Linux and macOS users can access their node using `kubectl debug`

or their private IP Address. Windows users should skip to the Windows Server Proxy section for a workaround to SSH via proxy.

#### Connect using kubectl debug

To create an interactive shell connection, use the `kubectl debug`

command to run a privileged container on your node.

To list your nodes, use the

`kubectl get nodes`

command:`kubectl get nodes -o wide`

Sample output:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE aks-nodepool1-37663765-vmss000000 Ready agent 166m v1.25.6 10.224.0.33 <none> Ubuntu 22.04.2 LTS aks-nodepool1-37663765-vmss000001 Ready agent 166m v1.25.6 10.224.0.4 <none> Ubuntu 22.04.2 LTS aksnpwin000000 Ready agent 160m v1.25.6 10.224.0.62 <none> Windows Server 2022 Datacenter`

Use the

`kubectl debug`

command to start a privileged container on your node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

You now have access to the node through a privileged container as a debugging pod.

Note

You can interact with the node session by running

`chroot /host`

from the privileged container.

#### Exit kubectl debug mode

When you're done with your node, enter the `exit`

command to end the interactive shell session. After the interactive container session closes, delete the debugging pod used with `kubectl delete pod`

.

```
kubectl delete pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx
```


### Windows Server proxy connection for SSH

Follow these steps as a workaround to connect with SSH on a Windows Server node.

#### Create a proxy server

At this time, you can't connect to a Windows Server node directly by using `kubectl debug`

. Instead, you need to first connect to another node in the cluster with `kubectl`

, then connect to the Windows Server node from that node using SSH.

To connect to another node in the cluster, use the `kubectl debug`

command. For more information, follow the above steps in the kubectl section. Create an SSH connection to the Windows Server node from another node using the SSH keys provided when you created the AKS cluster and the internal IP address of the Windows Server node.

Important

The following steps for creating the SSH connection to the Windows Server node from another node can only be used if you created your AKS cluster using the Azure CLI with the `--generate-ssh-keys`

parameter. If you want to use your own SSH keys instead, you can use the `az aks update`

to manage SSH keys on an existing AKS cluster. For more information, see [manage SSH node access](manage-ssh-node-access).

Note

If your Linux proxy node is down or unresponsive, use the [Azure Bastion](/en-us/azure/bastion/bastion-overview) method to connect instead.

Use the

`kubectl debug`

command to start a privileged container on your proxy (Linux) node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

Open a new terminal window and use the

`kubectl get pods`

command to get the name of the pod started by`kubectl debug`

.`kubectl get pods`

Sample output:

`NAME READY STATUS RESTARTS AGE node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 1/1 Running 0 21s`

In the sample output,

*node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx*is the name of the pod started by`kubectl debug`

.Use the

`kubectl port-forward`

command to open a connection to the deployed pod:`kubectl port-forward node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 2022:22`

Sample output:

`Forwarding from 127.0.0.1:2022 -> 22 Forwarding from [::1]:2022 -> 22`

The previous example begins forwarding network traffic from port

`2022`

on your development computer to port`22`

on the deployed pod. When using`kubectl port-forward`

to open a connection and forward network traffic, the connection remains open until you stop the`kubectl port-forward`

command.Open a new terminal and run the command

`kubectl get nodes`

to show the internal IP address of the Windows Server node:`kubectl get no -o custom-columns=NAME:metadata.name,'INTERNAL_IP:status.addresses[?(@.type == \"InternalIP\")].address'`

Sample output:

`NAME INTERNAL_IP aks-nodepool1-19409214-vmss000003 10.224.0.8`

In the previous example,

*10.224.0.62*is the internal IP address of the Windows Server node.Create an SSH connection to the Windows Server node using the internal IP address, and connect to port

`22`

through port`2022`

on your development computer. The default username for AKS nodes is*azureuser*. Accept the prompt to continue with the connection. You're then provided with the bash prompt of your Windows Server node:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' azureuser@10.224.0.62`

Sample output:

`The authenticity of host '10.224.0.62 (10.224.0.62)' can't be established. ECDSA key fingerprint is SHA256:1234567890abcdefghijklmnopqrstuvwxyzABCDEFG. Are you sure you want to continue connecting (yes/no)? yes`

Note

If you prefer to use password authentication, include the parameter

`-o PreferredAuthentications=password`

. For example:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' -o PreferredAuthentications=password azureuser@10.224.0.62`


## Use a host process container to access Windows node

Run the following script to create

`hostprocess.yaml`

. In the script, replace`AKSWINDOWSNODENAME`

with the AKS Windows node name.This specification uses the nanoserver base image. The base image doesn't have PowerShell, but because it runs as a host process container (HPC), PowerShell is available in the underlying VM.

`apiVersion: v1 kind: Pod metadata: labels: pod: hpc name: hpc spec: securityContext: windowsOptions: hostProcess: true runAsUserName: "NT AUTHORITY\\SYSTEM" hostNetwork: true containers: - name: hpc image: mcr.microsoft.com/windows/nanoserver:ltsc2022 # Use nanoserver:1809 for WS2019 command: - powershell.exe - -Command - "Start-Sleep 2147483" imagePullPolicy: IfNotPresent nodeSelector: kubernetes.io/os: windows kubernetes.io/hostname: AKSWINDOWSNODENAME tolerations: - effect: NoSchedule key: node.kubernetes.io/unschedulable operator: Exists - effect: NoSchedule key: node.kubernetes.io/network-unavailable operator: Exists - effect: NoExecute key: node.kubernetes.io/unreachable operator: Exists`

Run

`kubectl apply -f hostprocess.yaml`

to deploy the Windows HPC in the specified Windows node.Use

`kubectl exec -it [HPC-POD-NAME] -- powershell`

.You can run any PowerShell commands inside the HPC container to access the Windows node.


Note

You need to switch the root folder to `C:\`

inside the HPC container to access the files in the Windows node.

## SSH using Azure Bastion for Windows

If your Linux proxy node isn't reachable, using Azure Bastion as a proxy is an alternative. This method requires that you set up an Azure Bastion host for the virtual network in which the cluster resides. See [Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview) for more details.

## SSH using private IPs from the AKS API

If you don't have access to the Kubernetes API, you can get access to properties such as `Node IP`

and `Node Name`

through the [AKS agent pool API ](/en-us/rest/api/aks/agent-pools/get#agentpool), (available on stable versions `07-01-2024`

or above) to connect to AKS nodes.

### Create an interactive shell connection to a node using the IP address

For convenience, AKS nodes are exposed on the cluster's virtual network through private IP addresses. However, you need to be in the cluster's virtual network to SSH into the node. If you don't already have an environment configured, you can use [Azure Bastion](/en-us/azure/bastion/bastion-connect-vm-ssh-linux) to establish a proxy from which you can SSH to cluster nodes. Make sure the Azure Bastion is deployed in the same virtual network as the cluster.

Obtain private IPs using the

`az aks machine list`

command, targeting all the VMs in a specific node pool with the`--nodepool-name`

flag.`az aks machine list --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name nodepool1 -o table`

The following example output shows the internal IP addresses of all the nodes in the node pool:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4 aks-nodepool1-33555069-vmss000001 10.224.0.6 IPv4 aks-nodepool1-33555069-vmss000002 10.224.0.4 IPv4`

To target a specific node inside the node pool, use the

`--machine-name`

flag:`az aks machine show --cluster-name myAKScluster --nodepool-name nodepool1 -g myResourceGroup --machine-name aks-nodepool1-33555069-vmss000000 -o table`

The following example output shows the internal IP address of all the specified node:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4`

SSH to the node using the private IP address you obtained in the previous step. This step is applicable for Linux machines only. For Windows machines, see

[Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview).`ssh -i /path/to/private_key.pem azureuser@10.224.0.33`


## Next steps

If you need more troubleshooting data, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes control plane logs](monitor-aks-reference#resource-logs).

To learn about managing your SSH keys, see [Manage SSH configuration](manage-ssh-node-access).


---

<!-- DOCUMENTO FUSIONADO: _kms-data-encryption-concepts___istio-latency__troubleshooting_index_node-resour_5da6dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kms-data-encryption-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kms-data-encryption-concepts -->

# Data encryption at rest concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) stores sensitive data such as Kubernetes secrets in etcd, the distributed key-value store used by Kubernetes. For enhanced security and compliance requirements, AKS supports encryption of Kubernetes secrets at rest using the Kubernetes Key Management Service (KMS) provider integrated with Azure Key Vault.

This article explains the key concepts, encryption models, and key management options available for protecting Kubernetes secrets at rest in AKS.

## Understanding data encryption at rest

Data encryption at rest protects your data when it's stored on disk. Without encryption at rest, an attacker who gains access to the underlying storage could potentially read sensitive data like Kubernetes secrets.

AKS provides encryption for Kubernetes secrets stored in etcd:

| Layer | Description |
|---|---|
Azure platform encryption |
Azure Storage automatically encrypts all data at rest using 256-bit AES encryption. This encryption is always enabled and transparent to users. |
KMS provider encryption |
An optional layer that encrypts Kubernetes secrets before they're written to etcd using keys stored in Azure Key Vault. |

For more information about Azure's encryption at rest capabilities, see [Azure data encryption at rest](/en-us/azure/security/fundamentals/encryption-atrest) and [Azure encryption models](/en-us/azure/security/fundamentals/encryption-models).

## KMS provider for data encryption

The [Kubernetes KMS provider](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) is a mechanism that enables encryption of Kubernetes secrets at rest using an external key management system. AKS integrates with Azure Key Vault to provide this capability, giving you control over encryption keys while maintaining the security benefits of a managed Kubernetes service.

### How KMS encryption works

When you enable KMS for an AKS cluster:

**Secret creation**: When a secret is created, the Kubernetes API server sends the secret data to the KMS provider plugin.**Encryption**: The KMS plugin encrypts the secret data using a Data Encryption Key (DEK), which is itself encrypted using a Key Encryption Key (KEK) stored in Azure Key Vault.**Storage**: The encrypted secret is stored in etcd.**Secret retrieval**: When a secret is read, the KMS plugin decrypts the DEK using the KEK from Azure Key Vault, then uses the DEK to decrypt the secret data.

This envelope encryption approach provides both security and performance benefits. The DEK handles frequent encryption operations locally while the KEK in Azure Key Vault provides the security of a hardware-backed key management system.

## Key management options

AKS offers two key management options for KMS encryption:

### Platform-managed keys (PMK)

With platform-managed keys, AKS automatically manages the encryption keys for you:

- AKS creates and manages the encryption keys.
- Key rotation is handled automatically by the platform.
- No additional configuration or key vault setup is required.

**When to use platform-managed keys:**

- You want the simplest setup with minimal configuration.
- You don't have specific regulatory requirements that mandate customer-managed keys.
- You want automatic key rotation without manual intervention.

### Customer-managed keys (CMK)

With customer-managed keys, you have full control over the encryption keys:

- You create and manage your own Azure Key Vault and encryption keys.
- You control key rotation schedules and policies.

**When to use customer-managed keys:**

- You have regulatory or compliance requirements that mandate customer-managed keys.
- You need to control the key lifecycle, including rotation schedules and key versions.
- You require audit logs for all key operations.

### Key vault network access options

When using customer-managed keys, you can configure the network access for your Azure Key Vault:

| Network access | Description | Use case |
|---|---|---|
Public |
Key vault is accessible over the public internet with authentication. | Development environments, simpler setup |
Private |
Key vault has public network access disabled. AKS accesses the key vault through the
|

## Comparing encryption key options

| Feature | Platform-managed keys | Customer-managed keys (Public) | Customer-managed keys (Private) |
|---|---|---|---|
Key ownership |
Microsoft manages | Customer manages | Customer manages |
Key rotation |
Automatic |
|

[User configurable](/en-us/azure/key-vault/keys/how-to-configure-key-rotation)**Key vault creation****Network isolation**## Requirements

- The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience requires**Kubernetes version 1.33 or later**. - The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience is only supported on AKS clusters where[managed identity is used for the cluster's identity](use-managed-identity).

## Limitations

**No downgrade**: After enabling the new KMS encryption experience, you can't disable the feature.**Key deletion**: Deleting the encryption key or key vault makes your secrets unrecoverable.**Private endpoint access**: Key vault access using[private link/endpoint](/en-us/azure/key-vault/general/private-link-service)isn't yet supported. For private key vaults, use the[trusted services firewall exception](/en-us/azure/key-vault/general/network-security#key-vault-firewall-enabled-trusted-services-only).


---

<!-- DOCUMENTO FUSIONADO: __istio-latency__troubleshooting_index_node-resource-group-lockdown.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _istio-latency__troubleshooting_index.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-latency.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-latency -->

# Latency comparison across versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This document elaborates on the [data plane latency performance](istio-scale#data-plane-performance) across Istio add-on versions and Kubernetes version. The results evaluate the impact of adding sidecar proxies to the data path, showcasing the P90 and P99 latency difference. The comparison measures the difference between traffic routed through the sidecar and traffic sent directly to the pod.

- Traffic going through the sidecar: client --> client-sidecar --> server-sidecar --> server
- Traffic directly going to the pod: client --> server

## Test specifications

- Node SKU: Standard D16 v5 (16 vCPU, 64-GB memory)
- Two proxy workers
- 1-KB payload
- 1,000 Queries per second (QPS) at varying client connections
`http/1.1`

protocol and mutual Transport Layer Security (TLS) enabled

| P99 Latency Difference | P90 Latency Difference |
|---|---|
|


---

<!-- DOCUMENTO FUSIONADO: _troubleshooting_index.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: troubleshooting.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/troubleshooting -->

# Azure Kubernetes Service (AKS) troubleshooting documentation

Welcome to Azure Kubernetes Service troubleshooting. These articles explain how to determine, diagnose, and fix issues that you might encounter when you use Azure Kubernetes Service (AKS). In the navigation pane on the left, browse through the article list or use the search box to find issues and solutions.


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ -->

# Azure Kubernetes Service (AKS)

AKS allows you to quickly deploy a production ready Kubernetes cluster in Azure. Learn how to use AKS with these quickstarts, tutorials, and samples.

This browser is no longer supported.

Upgrade to Microsoft Edge to take advantage of the latest features, security updates, and technical support.

AKS allows you to quickly deploy a production ready Kubernetes cluster in Azure. Learn how to use AKS with these quickstarts, tutorials, and samples.


---

<!-- DOCUMENTO FUSIONADO: node-resource-group-lockdown.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-resource-group-lockdown -->

# Deploy a fully managed resource group using node resource group lockdown in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS deploys infrastructure into your subscription for connecting to and running your applications. Changes made directly to resources in the [node resource group](concepts-clusters-workloads#node-resource-group) can affect cluster operations or cause future issues. For example, scaling, storage, or network configurations should be made through the Kubernetes API and not directly on these resources.

To prevent changes from being made to the node resource group, you can apply a deny assignment and block users from modifying resources created as part of the AKS cluster.

## Before you begin

Before you begin, you need the following resources installed and configured:

- The Azure CLI version 2.44.0 or later. Run
`az --version`

to find the current version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an AKS cluster with node resource group lockdown

Create a cluster with node resource group lockdown using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--nrg-lockdown-restriction-level`

flag set to `ReadOnly`

. This configuration allows you to view the resources but not modify them.```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--nrg-lockdown-restriction-level ReadOnly \
--generate-ssh-keys
```


## Update an existing cluster with node resource group lockdown

Update an existing cluster with node resource group lockdown using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--nrg-lockdown-restriction-level`

flag set to `ReadOnly`

. This configuration allows you to view the resources but not modify them.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --nrg-lockdown-restriction-level ReadOnly
```


## Remove node resource group lockdown from a cluster

Remove node resource group lockdown from an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--nrg-restriction-level`

flag set to `Unrestricted`

. This configuration allows you to view and modify the resources.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --nrg-lockdown-restriction-level Unrestricted
```


## Next steps

To learn more about the node resource group in AKS, see [Node resource group](concepts-clusters-workloads#node-resource-group).
