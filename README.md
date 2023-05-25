# crossplane

![Version: 1.12.1-bb.0](https://img.shields.io/badge/Version-1.12.1--bb.0-informational?style=flat-square) ![AppVersion: 1.12.1](https://img.shields.io/badge/AppVersion-1.12.1-informational?style=flat-square)

Crossplane is an open source Kubernetes add-on that enables platform teams to assemble infrastructure from multiple vendors, and expose higher level self-service APIs for application teams to consume.

## Upstream References
* <https://crossplane.io>

## Learn More
* [Application Overview](docs/overview.md)
* [Other Documentation](docs/)

## Pre-Requisites

* Kubernetes Cluster deployed
* Kubernetes config installed in `~/.kube/config`
* Helm installed

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

* Clone down the repository
* cd into directory
```bash
helm install crossplane chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicas | int | `1` | The number of replicas to run for the Crossplane pods. |
| deploymentStrategy | string | `"RollingUpdate"` | The deployment strategy for the Crossplane and RBAC Manager (if enabled) pods. |
| image.repository | string | `"registry1.dso.mil/ironbank/opensource/crossplane/crossplane"` | Crossplane image. |
| image.tag | string | `""` | Crossplane image tag: if not set, appVersion field from Chart.yaml is used. |
| image.pullPolicy | string | `"IfNotPresent"` | Crossplane image pull policy used in all containers. |
| nodeSelector | object | `{}` | Enable nodeSelector for Crossplane pod. |
| tolerations | list | `[]` | Enable tolerations for Crossplane pod. |
| affinity | object | `{}` | Enable affinity for Crossplane pod. |
| hostNetwork | bool | `false` | Enable hostNetwork for Crossplane. Caution: setting it to true means Crossplane's Pod will have high privileges. |
| customLabels | object | `{}` | Custom labels to add into metadata. |
| customAnnotations | object | `{}` | Custom annotations to add to the Crossplane deployment and pod. |
| serviceAccount.customAnnotations | object | `{}` | Custom annotations to add to the serviceaccount of Crossplane. |
| leaderElection | bool | `true` | Enable leader election for Crossplane Managers pod. |
| args | list | `[]` | A list of additional args to be passed to Crossplane's container. |
| provider.packages | list | `[]` | The list of Provider packages to install together with Crossplane. |
| configuration.packages | list | `[]` | The list of Configuration packages to install together with Crossplane. |
| imagePullSecrets | list | `["private-registry"]` | Names of image pull secrets to use. imagePullSecrets: {} |
| registryCaBundleConfig.name | object | `{}` | Name of ConfigMap containing additional CA bundle for fetching from package registries. |
| registryCaBundleConfig.key | object | `{}` | Key to use from ConfigMap containing additional CA bundle for fetching from package registries. |
| webhooks.enabled | bool | `true` | Enable webhook functionality for Crossplane as well as packages installed by Crossplane. |
| rbacManager.deploy | bool | `true` | Deploy RBAC Manager and its required roles. |
| rbacManager.skipAggregatedClusterRoles | bool | `false` | Opt out of deploying aggregated ClusterRoles. |
| rbacManager.replicas | int | `1` | The number of replicas to run for the RBAC Manager pods. |
| rbacManager.managementPolicy | string | `"All"` | The extent to which the RBAC manager will manage permissions:. - `All` indicates to manage all Crossplane controller and user roles. - `Basic` indicates to only manage Crossplane controller roles and the `crossplane-admin`, `crossplane-edit`, and `crossplane-view` user roles. |
| rbacManager.leaderElection | bool | `true` | Enable leader election for RBAC Managers pod. |
| rbacManager.args | list | `[]` | A list of additional args to be pased to the RBAC manager's container. |
| rbacManager.nodeSelector | object | `{}` | Enable nodeSelector for RBAC Managers pod. |
| rbacManager.tolerations | list | `[]` | Enable tolerations for RBAC Managers pod. |
| rbacManager.affinity | object | `{}` | Enable affinity for RBAC Managers pod. |
| priorityClassName | string | `""` | Priority class name for Crossplane and RBAC Manager (if enabled) pods. |
| resourcesCrossplane.limits.cpu | string | `"100m"` | CPU resource limits for Crossplane. |
| resourcesCrossplane.limits.memory | string | `"512Mi"` | Memory resource limits for Crossplane. |
| resourcesCrossplane.requests.cpu | string | `"100m"` | CPU resource requests for Crossplane. |
| resourcesCrossplane.requests.memory | string | `"256Mi"` | Memory resource requests for Crossplane. |
| securityContextCrossplane.runAsUser | int | `65532` | Run as user for Crossplane. |
| securityContextCrossplane.runAsGroup | int | `65532` | Run as group for Crossplane. |
| securityContextCrossplane.allowPrivilegeEscalation | bool | `false` | Allow privilege escalation for Crossplane. |
| securityContextCrossplane.readOnlyRootFilesystem | bool | `true` | ReadOnly root filesystem for Crossplane. |
| packageCache.medium | string | `""` | Storage medium for package cache. `Memory` means volume will be backed by tmpfs, which can be useful for development. |
| packageCache.sizeLimit | string | `"20Mi"` | Size limit for package cache. If medium is `Memory` then maximum usage would be the minimum of this value the sum of all memory limits on containers in the Crossplane pod. |
| packageCache.pvc | string | `""` | Name of the PersistentVolumeClaim to be used as the package cache. Providing a value will cause the default emptyDir volume to not be mounted. |
| packageCache.configMap | string | `""` | Name of the ConfigMap to be used as package cache. Providing a value will cause the default emptyDir volume not to be mounted. |
| resourcesRBACManager.limits.cpu | string | `"100m"` | CPU resource limits for RBAC Manager. |
| resourcesRBACManager.limits.memory | string | `"512Mi"` | Memory resource limits for RBAC Manager. |
| resourcesRBACManager.requests.cpu | string | `"100m"` | CPU resource requests for RBAC Manager. |
| resourcesRBACManager.requests.memory | string | `"256Mi"` | Memory resource requests for RBAC Manager. |
| securityContextRBACManager.runAsUser | int | `65532` | Run as user for RBAC Manager. |
| securityContextRBACManager.runAsGroup | int | `65532` | Run as group for RBAC Manager. |
| securityContextRBACManager.allowPrivilegeEscalation | bool | `false` | Allow privilege escalation for RBAC Manager. |
| securityContextRBACManager.readOnlyRootFilesystem | bool | `true` | ReadOnly root filesystem for RBAC Manager. |
| metrics.enabled | bool | `false` | Expose Crossplane and RBAC Manager metrics endpoint. |
| extraEnvVarsCrossplane | object | `{}` | List of extra environment variables to set in the Crossplane deployment. Any `.` in variable names will be replaced with `_` (example: `SAMPLE.KEY=value1` becomes `SAMPLE_KEY=value1`). |
| extraEnvVarsRBACManager | object | `{}` | List of extra environment variables to set in the Crossplane rbac manager deployment. Any `.` in variable names will be replaced with `_` (example: `SAMPLE.KEY=value1` becomes `SAMPLE_KEY=value1`). |
| podSecurityContextCrossplane | object | `{}` | PodSecurityContext for Crossplane. |
| podSecurityContextRBACManager | object | `{}` | PodSecurityContext for RBAC Manager. |
| extraVolumesCrossplane | object | `{}` | List of extra Volumes to add to Crossplane. |
| extraVolumeMountsCrossplane | object | `{}` | List of extra volumesMounts to add to Crossplane. |
| xfn.enabled | bool | `false` | Enable alpha xfn sidecar container that runs Composition Functions. Note you also need to run Crossplane with --enable-composition-functions for it to call xfn. |
| xfn.image | object | `{"pullPolicy":"IfNotPresent","repository":"crossplane/xfn","tag":""}` | Image for xfn: if tag is not set appVersion field from Chart.yaml is used. |
| xfn.args | list | `[]` | List of additional args for the xfn container. |
| xfn.extraEnvVars | object | `{}` | List of additional environment variables for the xfn container. |
| xfn.securityContext.runAsUser | int | `65532` | Run as user for xfn sidecar. |
| xfn.securityContext.runAsGroup | int | `65532` | Run as group for xfn sidecar. |
| xfn.securityContext.allowPrivilegeEscalation | bool | `false` | Allow privilege escalation for xfn sidecar. |
| xfn.securityContext.readOnlyRootFilesystem | bool | `true` | ReadOnly root filesystem for xfn sidecar. |
| xfn.securityContext.capabilities | object | `{"add":["SETUID","SETGID"]}` | Capabilities configuration for xfn sidecar. These capabilities allow xfn sidecar to create better user namespaces. It drops them after creating a namespace. |
| xfn.securityContext.seccompProfile | object | `{"type":"Unconfined"}` | Seccomp Profile for xfn. xfn needs the unshare syscall, which most RuntimeDefault seccomp profiles do not allow. |
| xfn.cache | object | `{"configMap":"","medium":"","pvc":"","sizeLimit":"1Gi"}` | Cache configuration for xfn. |
| xfn.resources | object | `{"limits":{"cpu":"2000m","memory":"2Gi"},"requests":{"cpu":"1000m","memory":"1Gi"}}` | Resources definition for xfn. |
| xfn.resources.limits.cpu | string | `"2000m"` | CPU resource limits for RBAC Manager. |
| xfn.resources.limits.memory | string | `"2Gi"` | Memory resource limits for RBAC Manager. |
| xfn.resources.requests.cpu | string | `"1000m"` | CPU resource requests for RBAC Manager. |
| xfn.resources.requests.memory | string | `"1Gi"` | Memory resource requests for RBAC Manager. |
| istio.enabled | bool | `false` | Toggle istio integration |
| istio.mtls | object | `{"mode":"STRICT"}` | Default Crossplane peer authentication |
| istio.mtls.mode | string | `"STRICT"` | STRICT = Allow only mutual TLS traffic, PERMISSIVE = Allow both plain text and mutual TLS traffic |
| networkPolicies.enabled | bool | `false` | Toggle network policies |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
