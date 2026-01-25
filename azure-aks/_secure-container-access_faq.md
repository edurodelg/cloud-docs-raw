---
merged_at: 2026-01-25T12:25:33.979243
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: secure-container-access.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/secure-container-access -->

# Security container access to resources using built-in Linux security features

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to secure container access to resources for your Azure Kubernetes Service (AKS) workloads.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

You can use built-in Kubernetes *pod security contexts* to define more permissions, such as the user or group to run as, the Linux capabilities to expose, or setting `allowPrivilegeEscalation: false`

in the pod manifest. For more best practices, see [Secure pod access to resources](https://kubernetes.io/docs/concepts/security/pod-security-standards/).

To improve the host isolation and decrease lateral movement on Linux, you can use *user-namespaces*.

For even more granular control of container actions, you can use built-in Linux security features such as *AppArmor* and *seccomp*.

- Define Linux security features at the node level.
- Implement features through a pod manifest.

Built-in Linux security features are only available on Linux nodes and pods.

Note

Currently, Kubernetes environments aren't completely safe for hostile multitenant usage. Additional security features, like *Microsoft Defender for Containers*, *AppArmor*, *seccomp*, *user-namespaces*, *Pod Security Admission*, or *Kubernetes RBAC for nodes*, efficiently block exploits.

For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters.

## User-namespaces

Linux pods run using several namespaces by default: a network namespaces to isolate the network identity and a PID namespace to isolate the processes. A [user-namespace](https://man7.org/linux/man-pages/man7/user_namespaces.7.html) isolates the users inside the container from the users on the host. It also limits the scope of capabilities and the pod's interactions with the rest of the system.

The UIDs and GIDs inside the container are mapped to unprivileged users on the host, so all interaction with the rest of the host happen as those unprivileged UID and GID. For example, root inside the container (UID 0) can be mapped to user 65536 on the host. Kubernetes creates the mapping to guarantee it doesn't overlap with other pods using user-namespaces on the system.

The Kubernetes implementation has some key benefits:

**Increased host isolation**: If a container escapes the pod boundaries, even if it runs as root inside the container, it has no privileges on the host. The reason is because the UIDs and GIDs of the container are mapped to unprivileged users on the host. If there's a container escape, user-namespaces greatly protects what files on the host a container can read/write, which process it can send signals to. Capabilities granted are only valid inside the user namespace and not on the host.**Prevention of lateral movement**: As the UIDs and GIDs for different containers are mapped to different, nonoverlapping UIDs and GIDs on the host, containers have a harder time attacking each other. For example, suppose container A runs with different UIDs and GIDs on the host than container B. In case of a container breakout, the operations it can do on container B's files and processes are limited: only read/write what a file allows to others. But not even that ends up being possible, as there's an extra prevention on the parent directory of the pod root volume to make sure only the pod GID can access it.**Honor Least-privilege principle**: As the UIDs and GIDs are mapped to unprivileged users on the host, only users that need the privilege on the host (and disable user namespaces) get it. Without user namespaces, there's no separation between container's users and host's users. We can't avoid giving privileges on the host to processes that don't need it, when they need privilege just inside the container.**Enablement of new use cases**: User namespaces allow containers to gain certain capabilities inside their own user namespace without affecting the host. The capabilities granted restricted to the pod unlocks new possibilities, such as running applications that require privileged operations without granting full root access on the host. Common new use-cases that can be implemented securely are: running nested containers and unprivileged container builds.**Unprivileged container setup**: Most of the container creation and setup doesn't run as root on the host, which significantly limits the impact of many CVEs.

None of these things are true when user-namespaces aren't used. If the container runs as root, when user-namespaces aren't used, the process is running as root on the host, the capabilities are valid on the host and the container setup is done as root on the host.

### Before you begin

Before you begin, make sure you have the following:

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Minimum kubernetes version 1.33 for the control plane and worker nodes. If you're not using kubernetes version 1.33 or higher, you'll need to
[upgrade your kubernetes version](upgrade-aks-cluster). - Worker nodes running Azure Linux 3.0 or Ubuntu 24.04. If you're not using these OS versions, you will not have the minimum
[stack requirements](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/#before-you-begin)to enable user-namespaces. You'll need to[upgrade your OS version](upgrade-os-version).

### Limitations

- User-namespaces is a linux kernel feature and is not supported for Windows node pools.
- Don't hesitate to check the
[Kubernetes documentation for user namespaces](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/), in particular the limitations section.

### Enable user-namespaces

There are no configurations needed to use this feature. If using the required AKS version, everything works out of the box.

Create a file named

`mypod.yaml`

and copy in the following manifest:To use user-namespaces, the yaml needs to have the field

`hostUsers: false`

.`apiVersion: v1 kind: Pod metadata: name: userns spec: hostUsers: false containers: - name: shell command: ["sleep", "infinity"] image: debian`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f mypod.yaml`

Check the status of the deployed pods using the

`kubectl get pods`

command.`kubectl get pods`

Exec into the pod to check

`/proc/self/uid_map`

by using the`kubectl exec`

command:`kubectl exec -ti userns -- bash # Now inside the pod run cat /proc/self/uid_map`


The output should have 65536 in the last column. For example:

```
0 833617920 65536
```


### CVEs mitigated

Here are some CVEs that are completely/partially mitigated with user-namespaces.

Bear in mind the list isn't exhaustive, it's just a selection of CVEs with high score that are mitigated:

[CVE-2019-5736](https://nvd.nist.gov/vuln/detail/CVE-2019-5736)- Score 8.6 (HIGH)[CVE 2024-21262](https://github.com/opencontainers/runc/security/advisories/GHSA-xr7r-f8xq-vfvv): Score 8.6 (HIGH)[CVE 2022-0492](https://unit42.paloaltonetworks.com/cve-2022-0492-cgroups/): Score 7.8 (HIGH)[CVE-2021-25741](https://nvd.nist.gov/vuln/detail/CVE-2021-25741): Score: 8.1 (HIGH) / 8.8 (HIGH)[CVE-2017-1002101](https://nvd.nist.gov/vuln/detail/CVE-2017-1002101): Score: 9.6 (CRITICAL) / 8.8(HIGH)

To learn more, read this [blog post](https://kubernetes.io/blog/2025/04/25/userns-enabled-by-default/) with additional information around user-namespaces.

## App Armor

To limit container actions, you can use the [AppArmor](https://kubernetes.io/docs/tutorials/clusters/apparmor/) Linux kernel security module. AppArmor is available as part of the underlying AKS node OS and is enabled by default. You create AppArmor profiles that restrict read, write, or execute actions, or system functions like mounting filesystems. Default AppArmor profiles restrict access to various `/proc`

and `/sys`

locations and provide a means to logically isolate containers from the underlying node. AppArmor works for any application that runs on Linux, not just Kubernetes pods.

Note

Azure Linux 3.0 does not offer AppArmor support. For Azure Linux 3.0 nodes, the recommendation is to leverage SELinux instead of AppArmor for mandatory access control.

To see AppArmor in action, the following example creates a profile that prevents writing to files.

[SSH](manage-ssh-node-access)to an AKS node.Create a file named

*deny-write.profile*.Copy and paste the following content:

`#include <tunables/global> profile k8s-apparmor-example-deny-write flags=(attach_disconnected) { #include <abstractions/base> file, # Deny all file writes. deny /** w, }`


AppArmor profiles are added using the `apparmor_parser`

command.

Add the profile to AppArmor.

Specify the name of the profile created in the previous step:

`sudo apparmor_parser deny-write.profile`

If the profile is correctly parsed and applied to AppArmor, you won't see any output and you'll return to the command prompt.

From your local machine, create a pod manifest named

*aks-apparmor.yaml*. This manifest:- Defines an annotation for
`container.apparmor.security.beta.kubernetes`

. - References the
*deny-write*profile created in the previous steps.

`apiVersion: v1 kind: Pod metadata: name: hello-apparmor annotations: container.apparmor.security.beta.kubernetes.io/hello: localhost/k8s-apparmor-example-deny-write spec: containers: - name: hello image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: [ "sh", "-c", "echo 'Hello AppArmor!' && sleep 1h" ]`

- Defines an annotation for
With the pod deployed, run the following command and verify the

*hello-apparmor*pod shows a*Running*status:`kubectl get pods NAME READY STATUS RESTARTS AGE aks-ssh 1/1 Running 0 4m2s hello-apparmor 0/1 Running 0 50s`


For more information about AppArmor, see [AppArmor profiles in Kubernetes](https://kubernetes.io/docs/tutorials/clusters/apparmor/).

## Secure computing (seccomp)

While AppArmor works for any Linux application, [seccomp ( secure computing)](https://kubernetes.io/docs/reference/node/seccomp/) works at the process level. Seccomp is also a Linux kernel security module and is natively supported by the

`containerd`

runtime used by AKS nodes. With seccomp, you can limit a container's system calls. Seccomp establishes an extra layer of protection against common system call vulnerabilities exploited by malicious actors and allows you to specify a default profile for all workloads in the node.### Configure a default seccomp profile (preview)

You can apply default seccomp profiles using [custom node configurations](/en-us/azure/aks/custom-node-configuration) when creating a new Linux node pool. There are two values supported on AKS: `RuntimeDefault`

and `Unconfined`

. Some workloads might require a lower number of syscall restrictions than others. This means that they can fail during runtime with the 'RuntimeDefault' profile. To mitigate such a failure, you can specify the `Unconfined`

profile. If your workload requires a custom profile, see [Configure a custom seccomp profile](#configure-a-custom-seccomp-profile).

#### Limitations

- SeccompDefault is not a supported parameter for windows node pools.
- SeccompDefault is available starting in 2024-09-02-preview API.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

#### Register the `KubeletDefaultSeccompProfilePreview`

feature flag

Register the

`KubeletDefaultSeccompProfilePreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


#### Restrict your container's system calls with seccomp

**1. Follow steps to apply a seccomp profile in your kubelet configuration by specifying "seccompDefault": "RuntimeDefault"**.


`RuntimeDefault`

uses containerd's default seccomp profile, restricting certain system calls to enhance security. Restricted syscalls will fail. For more information, see the [containerD default seccomp profile](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51).

**2. Check that the configuration was applied**.

You can confirm the settings are applied to the nodes by [connecting to the host](node-access) and verifying configuration changes have been made on the filesystem.

**3. Troubleshoot workload failures**.

When SeccompDefault is enabled, the container runtime default seccomp profile is used by default for all workloads scheduled on the node. This might cause workloads to fail due to blocked syscalls. If a workload failure has occurred, you might see errors such as:

- Workload is existing unexpectedly after the feature is enabled, with "permission denied" error.
- Seccomp error messages can also be seen in auditd or syslog by replacing SCMP_ACT_ERRNO with SCMP_ACT_LOG in the default profile.

If you experience the above errors, we recommend that you change your seccomp profile to `Unconfined`

. `Unconfined`

places no restrictions on syscalls, allowing all system calls, which reduces security.

### Configure a custom seccomp profile

With a custom seccomp profile, you can have more granular control over restricted syscalls. Align to the best practice of granting the container minimal permission only to run by:

- Defining with filters what actions to allow or deny.
- Annotating within a pod YAML manifest to associate with the seccomp filter.

To see seccomp in action, create a filter that prevents changing permissions on a file.

[SSH](manage-ssh-node-access)to an AKS node.Create a seccomp filter named

*/var/lib/kubelet/seccomp/prevent-chmod*.Copy and paste the following content:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "name": "chmod", "action": "SCMP_ACT_ERRNO" }, { "name": "fchmodat", "action": "SCMP_ACT_ERRNO" }, { "name": "chmodat", "action": "SCMP_ACT_ERRNO" } ] }`

In version 1.19 and later, you need to configure:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "names": ["chmod","fchmodat","chmodat"], "action": "SCMP_ACT_ERRNO" } ] }`

From your local machine, create a pod manifest named

*aks-seccomp.yaml*and paste the following content. This manifest:- Defines an annotation for
`seccomp.security.alpha.kubernetes.io`

. - References the
*prevent-chmod*filter created in the previous step.

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented annotations: seccomp.security.alpha.kubernetes.io/pod: localhost/prevent-chmod spec: containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

In version 1.19 and later, you need to configure:

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented spec: securityContext: seccompProfile: type: Localhost localhostProfile: prevent-chmod containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

- Defines an annotation for
Deploy the sample pod using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f ./aks-seccomp.yaml`

View pod status using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.- The pod reports an error.
- The
`chmod`

command is prevented from running by the seccomp filter, as shown in the example output:

`kubectl get pods NAME READY STATUS RESTARTS AGE chmod-prevented 0/1 Error 0 7s`


For help troubleshooting your seccomp profile see the article [Troubleshoot seccomp profile configuration in Azure Kubernetes Service](/en-us/troubleshoot/azure/azure-kubernetes/security/troubleshoot-seccomp-profiles).

## Seccomp security profile options

Seccomp security profiles are a set of defined syscalls that are allowed or restricted. Most container runtimes have a default seccomp profile that is similar if not the same as the one Docker uses. For more information about available profiles, see [Docker](https://kubernetes.io/docs/reference/node/seccomp/) or [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profiles.

AKS uses the [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profile for our RuntimeDefault when you configure seccomp using [custom node configuration](/en-us/azure/aks/custom-node-configuration).

### Significant syscalls blocked by default profile

Both [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) maintain allowlists of safe syscalls. This table lists the significant (but not all) syscalls that are effectively blocked because they aren't on the allowlist. If any of the blocked syscalls are required by your workload, don't use the `RuntimeDefault`

seccomp profile.

When changes are made to [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51), AKS updates their default configuration to match. Updates to this list may cause workload failure. For release updates, see [AKS release notes](https://github.com/Azure/AKS/releases).

| Blocked syscall | Description |
|---|---|
`acct` |
Accounting syscall which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_PACCT` . |
`add_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`bpf` |
Deny loading potentially persistent bpf programs into kernel, already gated by `CAP_SYS_ADMIN` . |
`clock_adjtime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clock_settime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clone` |
Deny cloning new namespaces. Also gated by `CAP_SYS_ADMIN for CLONE_*` flags, except `CLONE_NEWUSER` . |
`create_module` |
Deny manipulation and functions on kernel modules. Obsolete. Also gated by `CAP_SYS_MODULE` . |
`delete_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`finit_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`get_kernel_syms` |
Deny retrieval of exported kernel and module symbols. Obsolete. |
`get_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`init_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`ioperm` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`iopl` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`kcmp` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`kexec_file_load` |
Sister syscall of kexec_load that does the same thing, slightly different arguments. Also gated by `CAP_SYS_BOOT` . |
`kexec_load` |
Deny loading a new kernel for later execution. Also gated by `CAP_SYS_BOOT` . |
`keyctl` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`lookup_dcookie` |
Tracing/profiling syscall, which could leak information on the host. Also gated by `CAP_SYS_ADMIN` . |
`mbind` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`mount` |
Deny mounting, already gated by `CAP_SYS_ADMIN` . |
`move_pages` |
Syscall that modifies kernel memory and NUMA settings. |
`nfsservctl` |
Deny interaction with the kernel nfs daemon. Obsolete since Linux 3.1. |
`open_by_handle_at` |
Cause of an old container breakout. Also gated by `CAP_DAC_READ_SEARCH` . |
`perf_event_open` |
Tracing/profiling syscall, which could leak information on the host. |
`personality` |
Prevent container from enabling BSD emulation. Not inherently dangerous, but poorly tested, potential for kernel vulns. |
`pivot_root` |
Deny pivot_root, should be privileged operation. |
`process_vm_readv` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`process_vm_writev` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`ptrace` |
Tracing/profiling syscall. Blocked in Linux kernel versions before 4.8 to avoid seccomp bypass. Tracing/profiling arbitrary processes is already blocked by dropping CAP_SYS_PTRACE, because it could leak information on the host. |
`query_module` |
Deny manipulation and functions on kernel modules. Obsolete. |
`quotactl` |
Quota syscall which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_ADMIN` . |
`reboot` |
Don't let containers reboot the host. Also gated by `CAP_SYS_BOOT` . |
`request_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`set_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`setns` |
Deny associating a thread with a namespace. Also gated by `CAP_SYS_ADMIN` . |
`settimeofday` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`stime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`swapon` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`swapoff` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`sysfs` |
Obsolete syscall. |
`_sysctl` |
Obsolete, replaced by /proc/sys. |
`umount` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`umount2` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`unshare` |
Deny cloning new namespaces for processes. Also gated by `CAP_SYS_ADMIN` , with the exception of unshare --user. |
`uselib` |
Older syscall related to shared libraries, unused for a long time. |
`userfaultfd` |
Userspace page fault handling, largely needed for process migration. |
`ustat` |
Obsolete syscall. |
`vm86` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |
`vm86old` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |

## Next steps

For associated best practices, see [Best practices for cluster security and upgrades in AKS](operator-best-practices-cluster-security) and [Best practices for pod security in AKS](developer-best-practices-pod-security).


---

<!-- DOCUMENTO FUSIONADO: faq.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/faq -->

# AKS frequently asked questions

This article provides answers to some of the most common questions about Azure Kubernetes Service (AKS).

## Support

### Does AKS offer a service-level agreement?

AKS provides service-level agreement (SLA) guarantees in the [Standard pricing tier with the Uptime SLA feature](free-standard-pricing-tiers).

### What is platform support, and what does it include?

Platform support is a reduced support plan for unsupported n-3 version clusters. Platform support includes only Azure infrastructure support.

For more information, see the [platform support policy](supported-kubernetes-versions).

### Does AKS automatically upgrade my unsupported clusters?

Yes, AKS initiates auto-upgrades for unsupported clusters. When a cluster in an n-3 version (where *n* is the latest supported AKS minor version that's generally available) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support policy.

For more information, see [Supported Kubernetes versions](supported-kubernetes-versions), [Planned maintenance windows](planned-maintenance), and [Automatic upgrades](auto-upgrade-cluster).

### Can I apply Azure reservation discounts to my AKS agent nodes?

AKS agent nodes are billed as standard Azure virtual machines (VMs). If you purchased [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations) for the VM size that you're using in AKS, those discounts are automatically applied.

## Operations

### Can I run Windows Server containers on AKS?

Yes, AKS supports Windows Server containers. For more information, see the [Windows Server on AKS FAQ](windows-faq).

### What Linux operating systems (OS) are supported on AKS?

AKS supports four main Linux operating systems, including Ubuntu Linux, [Azure Linux](use-azure-linux), [Azure Linux OS Guard](use-azure-linux-os-guard), and [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks). When specifying `--os-type Linux`

during node pool creation or cluster creation, the default OS is Ubuntu Linux.

### What operating systems (OS) versions are supported on AKS?

When using `--os-sku Ubuntu`

, AKS defaults to Ubuntu 22.04 in Kubernetes versions 1.25-1.34. AKS defaults to Ubuntu 24.04 in Kubernetes versions 1.35+.
When using `--os-sku AzureLinux`

, AKS defaults to Azure Linux 3.0 in Kubernetes versions 1.32+.
In some scenarios, like FIPS-enabled node pools, the default OS version might differ. See [node images](node-images) for more information.

### Can I move or migrate my cluster between Azure tenants?

No. Moving your AKS cluster between tenants is currently unsupported.

### Can I move or migrate my cluster between subscriptions?

No. Moving your AKS cluster between subscriptions is currently unsupported.

### Can I move my AKS cluster or AKS infrastructure resources to other resource groups or rename them?

No. Moving or renaming your AKS cluster and its associated resources isn't supported.

### Can I restore my cluster after I delete it?

No. You can't restore your cluster after you delete it. When you delete your cluster, the node resource group and all its resources are also deleted.

If you want to keep any of your resources, move them to another resource group before you delete your cluster. If you want to protect against accidental deletes, you can lock the AKS managed resource group that's hosting your cluster resources by using [Node resource group lockdown](node-resource-group-lockdown).

### Can I scale my AKS cluster to zero?

You can completely [stop a running AKS cluster](start-stop-cluster) or [scale or autoscale all or specific User node pools](scale-cluster#scale-user-node-pools-to-0) to zero.

You can't directly scale [system node pools](use-system-pools) to zero.

### Can I use the virtual machine scale set APIs to scale manually?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS APIs (`az aks scale`

).

### Can I use virtual machine scale sets to manually scale to zero nodes?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS API to scale nonsystem node pools to zero or [stop your cluster](start-stop-cluster) instead.

### Can I stop or deallocate all my VMs?

No. This configuration isn't supported. [Stop your cluster](start-stop-cluster) instead.

### Why are two resource groups created with AKS?

AKS builds upon many Azure infrastructure resources, including virtual machine scale sets, virtual networks, and managed disks. These integrations enable you to apply many of the core capabilities of the Azure platform within the managed Kubernetes environment provided by AKS. For example, you can use most Azure VM types directly with AKS, and you can use Azure Reservations to receive discounts on those resources automatically.

To enable this architecture, each AKS deployment spans two resource groups:

- You create the first resource group. This group contains only the Kubernetes service resource. The AKS resource provider automatically creates the second resource group during deployment. An example of the second resource group is
*MC_myResourceGroup_myAKSCluster_eastus*. For information on how to specify the name of this second resource group, see the next section. - The second resource group, known as the
*node resource group*, contains all of the infrastructure resources associated with the cluster. These resources include the Kubernetes node VMs, virtual networking, and storage. By default, the node resource group has a name like*MC_myResourceGroup_myAKSCluster_eastus*. AKS automatically deletes the node resource group whenever you delete the cluster. Use this resource group only for resources that share the cluster's lifecycle.

Note

Modifying any resource under the node resource group in the AKS cluster is an unsupported action and will cause cluster operation failures. You can prevent changes from being made to the node resource group. [Block users from modifying resources](node-resource-group-lockdown) that the AKS cluster manages.

### Can I provide my own name for the AKS node resource group?

By default, AKS names the node resource group *MC_resourcegroupname_clustername_location*, but you can provide your own name.

To specify your own resource group name, install the [aks-preview](/en-us/cli/azure/aks) Azure CLI extension version *0.3.2* or later. When you create an AKS cluster by using the `az aks create`

command, use the `--node-resource-group`

parameter and specify a name for the resource group. If you use an [Azure Resource Manager template](/en-us/azure/templates/microsoft.containerservice/2022-09-01/managedclusters) to deploy an AKS cluster, you can define the resource group name by using the `nodeResourceGroup`

property.

- The Azure resource provider automatically creates the secondary resource group.
- You can specify a custom resource group name only when you create the cluster.

As you work with the node resource group, you can't:

- Specify an existing resource group for the node resource group.
- Specify a different subscription for the node resource group.
- Change the node resource group name after you create the cluster.
- Specify names for the managed resources within the node resource group.
- Modify or delete Azure-created tags of managed resources within the node resource group.

### Can I modify tags and other properties of the AKS resources in the node resource group?

You might get unexpected scaling and upgrading errors if you modify or delete Azure-created tags and other resource properties in the node resource group. AKS allows you to create and modify custom tags created by end users, and you can add those tags when you [create a node pool](manage-node-pools#specify-a-taint-label-or-tag-for-a-node-pool). You might want to create or modify custom tags, for example, to assign a business unit or cost center. Another option is to apply policies and modify tags through the AKS resource itself—specifically via the cluster and node pools..

Azure-created tags are created for their respective Azure services, and you should always allow them. For AKS, there are the `aks-managed`

and `k8s-azure`

tags. Modifying any *Azure-created tags* on resources under the node resource group in the AKS cluster is an unsupported action, which breaks the service-level objective (SLO).

Note

In the past, the tag name `Owner`

was reserved for AKS to manage the public IP that's assigned on the front-end IP of the load balancer. Now, services use the `aks-managed`

prefix. For legacy resources, don't use Azure policies to apply the `Owner`

tag name. Otherwise, all resources on your AKS cluster deployment and update operations will break. This restriction doesn't apply to newly created resources.

### Why do I see aks-managed prefixed Helm releases on my cluster, and why does their revision count keep increasing?

AKS uses Helm to deliver components to your cluster. You can safely ignore `aks-managed`

prefixed Helm releases. Continuously increasing revisions on these Helm releases are expected and safe.

## Quotas, limits, and region availability

### Which Azure regions currently provide AKS?

For a complete list of available regions, see [AKS regions and availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

### Can I spread an AKS cluster across regions?

No. AKS clusters are regional resources and can't span regions. For guidance on how to create an architecture that includes multiple regions, see [best practices for business continuity and disaster recovery](operator-best-practices-multi-region#plan-for-multiregion-deployment).

### Can I spread an AKS cluster across availability zones?

Yes, you can deploy an AKS cluster across one or more [availability zones](availability-zones) in [regions that support them](/en-us/azure/reliability/availability-zones-region-support).

### Can I have different VM sizes in a single cluster?

Yes, you can use different VM sizes in your AKS cluster by creating [multiple node pools](create-node-pools).

### What's the size limit on a container image in AKS?

AKS doesn't set a limit on the container image size. But the larger the image, the higher the memory demand. A larger size could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is excessively large, as in the terabyte (TB) range, the kubelet might not be able to pull it from your container registry to a node because of the lack of disk space.

For Windows Server nodes, Windows Update doesn't automatically run and apply the latest updates. You should perform an upgrade on the cluster and the Windows Server node pools in your AKS cluster. Follow a regular schedule based on the Windows Update release cycle and your own validation process. This upgrade process creates nodes that run the latest Windows Server image and patches, and then removes the older nodes. For more information on this process, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

### Are AKS images required to run as root?

The following images have functional requirements to run as root, and exceptions must be filed for any policies:

*mcr.microsoft.com/oss/kubernetes/coredns**mcr.microsoft.com/azuremonitor/containerinsights/ciprod**mcr.microsoft.com/oss/calico/node**mcr.microsoft.com/oss/kubernetes-csi/azuredisk-csi*

## Security, access, and identity

### Can I limit who has access to the Kubernetes API server?

Yes, there are two options for limiting access to the API server:

- Use
[API server authorized IP ranges](api-server-authorized-ip-ranges)if you want to maintain a public endpoint for the API server but restrict access to a set of trusted IP ranges. - Use a
[private cluster](private-clusters)if you want to limit the API server to be accessible*only*from within your virtual network.

### Are security updates applied to AKS agent nodes?

AKS patches CVEs that have a *vendor fix* every week. CVEs without a fix are waiting on a vendor fix before they can be remediated. The AKS images are automatically updated within 30 days. We recommend that you apply an updated node image on a regular cadence to ensure that the latest patched images and OS patches are all applied and current. You can do this task:

- Manually, through the Azure portal or the Azure CLI.
- By upgrading your AKS cluster. The cluster upgrades
[cordon and drain nodes](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)automatically. Then it brings a new node online with the latest Ubuntu image and a new patch version or a minor Kubernetes version. For more information, see[Upgrade an AKS cluster](upgrade-cluster). - By using a
[node image upgrade](node-image-upgrade).

### Are there security threats that target AKS that I should be aware of?

Microsoft provides guidance for other actions that you can take to secure your workloads through services like [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks). For information on a security threat related to AKS and Kubernetes, see [New large-scale campaign targets Kubeflow](https://techcommunity.microsoft.com/t5/azure-security-center/new-large-scale-campaign-targets-kubeflow/ba-p/2425750) (June 8, 2021).

### Does AKS store any customer data outside the cluster's region?

No. All data is stored in the cluster's region.

### How can I avoid permission ownership setting slow issues when the volume has numerous files?

Traditionally, if your pod is running as a nonroot user (which it should), you must specify an `fsGroup`

parameter inside the pod's security context so that the volume is readable and writable by the pod. For more information on this requirement, see [Configure a security context for a pod or container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/).

A side effect of setting `fsGroup`

is that each time a volume is mounted, Kubernetes must use the `chown()`

and `chmod()`

commands recursively for all the files and directories inside the volume (with a few exceptions). This scenario happens even if group ownership of the volume already matches the requested `fsGroup`

parameter. This configuration might be expensive for larger volumes with lots of small files, which can cause pod startup to take a long time. This scenario was a known problem before v1.20. The workaround is to set the pod to run as root:

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
runAsUser: 0
fsGroup: 0
```


The issue was resolved with Kubernetes version 1.20. For more information, see [Kubernetes 1.20: Granular control of volume permission changes](https://kubernetes.io/blog/2020/12/14/kubernetes-release-1.20-fsgroupchangepolicy-fsgrouppolicy/).

## Networking

### How does the managed control plane communicate with my nodes?

AKS uses a secure tunnel communication to allow the `api-server`

and individual node kubelets to communicate, even on separate virtual networks. The tunnel is secured through mutual Transport Layer Security encryption. The current main tunnel that AKS uses is [Konnectivity, previously known as apiserver-network-proxy](https://kubernetes.io/docs/tasks/extend-kubernetes/setup-konnectivity/). Verify that all network rules follow the [Azure required network rules and fully qualified domain names (FQDNs)](limit-egress-traffic).

### Can my pods use the API server FQDN instead of the cluster IP?

Yes, you can add the annotation `kubernetes.azure.com/set-kube-service-host-fqdn`

to pods to set the `KUBERNETES_SERVICE_HOST`

variable to the domain name of the API server instead of the in-cluster service IP. This modification is useful in cases where your cluster egress is done via a layer 7 firewall. An example is when you use Azure Firewall with application rules.

### Can I configure NSGs with AKS?

AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. AKS modifies only the network interface NSG settings. If you're using Container Network Interface (CNI), you also must ensure that the security rules in the NSGs allow traffic between the node and pod classless interdomain routing (CIDR) ranges. If you're using kubenet, you must also ensure that the security rules in the NSGs allow traffic between the node and pod CIDR. For more information, see [Network security groups](concepts-network#network-security-groups).

### How does time synchronization work in AKS?

AKS nodes run the chrony service, which pulls time from the local host. Containers that run on pods get the time from the AKS nodes. Applications that open inside a container use time from the container of the pod.

## Add-ons, extensions, and integrations

### Can I use custom VM extensions?

No. AKS is a managed service. Manipulation of the infrastructure as a service (IaaS) resources isn't supported. To install custom components, use the Kubernetes APIs and mechanisms. For example, use DaemonSets to install any required components.

### What Kubernetes admission controllers does AKS support? Can admission controllers be added or removed?

AKS supports the following [admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/):

`NamespaceLifecycle`

`LimitRanger`

`ServiceAccount`

`DefaultIngressClass`

`DefaultStorageClass`

`DefaultTolerationSeconds`

`MutatingAdmissionWebhook`

`ValidatingAdmissionWebhook`

`ResourceQuota`

`PodNodeSelector`

`PodTolerationRestriction`

`ExtendedResourceToleration`


Currently, you can't modify the list of admission controllers in AKS.

### Can I use admission controller webhooks on AKS?

Yes, you can use admission controller webhooks on AKS. We recommend that you exclude internal AKS namespaces, which are marked with the `control-plane`

label. For example:

```
namespaceSelector:
matchExpressions:
- key: control-plane
operator: DoesNotExist
```


AKS firewalls the API server egress so that your admission controller webhooks need to be accessible from within the cluster.

### Can admission controller webhooks affect kube-system and internal AKS namespaces?

To protect the stability of the system and prevent custom admission controllers from affecting internal services in the `kube-system`

namespace, AKS has an admissions enforcer, which automatically excludes `kube-system`

and AKS internal namespaces. This service ensures that the custom admission controllers don't affect the services that run in `kube-system`

.

If you have a critical use case for deploying something on `kube-system`

(not recommended) in support of your custom admission webhook, you can add the following label or annotation so that the admissions enforcer ignores it:

- Label:
`"admissions.enforcer/disabled": "true"`

- Annotation:
`"admissions.enforcer/disabled": true`


### Is Azure Key Vault integrated with AKS?

[Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-driver) provides native integration of Azure Key Vault into AKS.

### Can I use FIPS cryptographic libraries with deployments on AKS?

Nodes that are enabled with Federal Information Processing Standards (FIPS) are now supported on Linux-based node pools. For more information, see [Add a FIPS-enabled node pool](enable-fips-nodes).

### How are AKS add-ons updated?

Any patch, including a security patch, is automatically applied to the AKS cluster. Anything bigger than a patch, like major or minor version changes (which can have breaking changes to your deployed objects), are updated when you update your cluster if a new release is available. For information on when a new release is available, see [AKS release notes](https://github.com/Azure/AKS/releases).

### What is the purpose of the AKS Linux extension that I see installed on my Linux virtual machine scale sets instances?

The AKS Linux extension is an Azure VM extension that installs and configures monitoring tools on Kubernetes worker nodes. The extension is installed on all new and existing Linux nodes. It configures the following monitoring tools:

[Node-exporter](https://github.com/prometheus/node_exporter): Collects hardware telemetry from the VM and makes it available by using a metrics endpoint. Then, a monitoring tool, such as Prometheus, can scrap these metrics.[Node-problem-detector](https://github.com/kubernetes/node-problem-detector): Aims to make various node problems visible to upstream layers in the cluster management stack. It's a systemd unit that runs on each node, detects node problems, and reports them to the cluster's API server by using`Events`

and`NodeConditions`

.[ig](https://go.microsoft.com/fwlink/p/?linkid=2260320): Is an eBPF-powered open-source framework for debugging and observing Linux and Kubernetes systems. It provides a set of tools (or gadgets) that gather relevant information that users can use to identify the cause of performance issues, crashes, or other anomalies. Notably, its independence from Kubernetes enables users to employ it also for debugging control plane issues.

These tools help provide observability around many node health-related problems, such as:

**Infrastructure daemon issues:**NTP service down**Hardware issues:**Bad CPU, memory, or disk**Kernel issues:**Kernel deadlock, corrupted file system**Container runtime issues:**Unresponsive runtime daemon

The extension *doesn't require extra outbound access* to any URLs, IP addresses, or ports beyond the [documented AKS egress requirements](limit-egress-traffic). It doesn't require any special permissions granted in Azure. It uses `kubeconfig`

to connect to the API server to send the monitoring data that's collected.

## Troubleshoot cluster issues

### Why is it taking so long to delete my cluster?

Most clusters are deleted upon user request. In some cases, especially cases where you bring your own resource group or perform cross-resource group tasks, deletion can take more time or even fail. If you have an issue with deletions, double-check that you don't have locks on the resource group. Also make sure that any resources outside the resource group are disassociated from the resource group.

### Why is it taking so long to create or update my cluster?

If you have issues with creating and updating clusters, make sure that you don't have any assigned policies or service constraints that might block your AKS cluster from managing resources like VMs, load balancers, or tags.

### If I have pods or deployments in NodeLost or Unknown states, can I still upgrade my cluster?

You can, but we don't recommend it. Perform updates when the state of the cluster is known and healthy.

### If I have a cluster with one or more nodes in an Unhealthy state, or if it's shut down, can I perform an upgrade?

No. Delete or remove any nodes that are in a failed state or otherwise from the cluster before you upgrade.

### I tried to delete my cluster, but I see the error "[Errno 11001] getaddrinfo failed."

Most commonly, this error arises if you have one or more NSGs in use that are still associated with the cluster. Remove them and attempt to delete the cluster again.

### I ran an upgrade, but now my pods are in crash loops and readiness probes fail.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

### My cluster was working, but suddenly I can't provision load balancers or mount persistent volume claims.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

## Retirements and deprecations

### Which Linux OS versions are deprecated on AKS?

Ubuntu 16.04 and Ubuntu 18.04 are no longer supported on AKS.
Starting on 17 March 2027, AKS will no longer support Ubuntu 20.04. For more information on this retirement, see [Retirement: Ubuntu 20.04 node pools on AKS](https://github.com/Azure/AKS/issues/4874).

### Which Windows OS versions are deprecated on AKS?

Starting on 1 March 2026, AKS will no longer support Windows Server 2019 node pools. Kubernetes versions 1.33+ can't use Windows Server 2019. For more information on this retirement, see [Retirement: Windows Server 2019 node pools on AKS](https://github.com/Azure/AKS/issues/4091).
Starting on 15 March 2027, AKS will no longer support Windows Server 2022 node pools. Kubernetes versions 1.36+ can't use Windows Server 2022. For more information on this retirement, see [Retirement: Windows Server 2022 node pools on AKS](https://github.com/Azure/AKS/issues/4168).
