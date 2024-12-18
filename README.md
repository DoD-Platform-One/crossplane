<!-- Warning: Do not manually edit this file. See notes on gluon + helm-docs at the end of this file for more information. -->
# crossplane

![Version: 1.18.1-bb.0](https://img.shields.io/badge/Version-1.18.1--bb.0-informational?style=flat-square) ![AppVersion: 1.18.1](https://img.shields.io/badge/AppVersion-1.18.1-informational?style=flat-square) ![Maintenance Track: unknown](https://img.shields.io/badge/Maintenance_Track-unknown-red?style=flat-square)

Crossplane is an open source Kubernetes add-on that enables platform teams to assemble infrastructure from multiple vendors, and expose higher level self-service APIs for application teams to consume.

## Upstream References
- <https://crossplane.io>

## Upstream Release Notes

- [Crossplane Release Notes](https://github.com/crossplane/crossplane/releases/tag/v1.18.1)

## Learn More

- [Application Overview](docs/overview.md)
- [Other Documentation](docs/)

## Pre-Requisites

- Kubernetes Cluster deployed
- Kubernetes config installed in `~/.kube/config`
- Helm installed

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

- Clone down the repository
- cd into directory

```bash
helm install crossplane chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicas | int | `1` | The number of Crossplane pod `replicas` to deploy. |
| revisionHistoryLimit | string | `nil` | The number of Crossplane ReplicaSets to retain. |
| deploymentStrategy | string | `"RollingUpdate"` | The deployment strategy for the Crossplane and RBAC Manager pods. |
| image.repository | string | `"registry1.dso.mil/ironbank/opensource/crossplane/crossplane"` | Repository for the Crossplane pod image. |
| image.tag | string | `""` | The Crossplane image tag. Defaults to the value of `appVersion` in `Chart.yaml`. |
| image.pullPolicy | string | `"IfNotPresent"` | The image pull policy used for Crossplane and RBAC Manager pods. |
| nodeSelector | object | `{}` | Add `nodeSelectors` to the Crossplane pod deployment. |
| tolerations | list | `[]` | Add `tolerations` to the Crossplane pod deployment. |
| affinity | object | `{}` | Add `affinities` to the Crossplane pod deployment. |
| topologySpreadConstraints | list | `[]` | Add `topologySpreadConstraints` to the Crossplane pod deployment. |
| hostNetwork | bool | `false` | Enable `hostNetwork` for the Crossplane deployment. Caution: enabling `hostNetwork` grants the Crossplane Pod access to the host network namespace. Consider setting `dnsPolicy` to `ClusterFirstWithHostNet`. |
| dnsPolicy | string | `""` | Specify the `dnsPolicy` to be used by the Crossplane pod. |
| customLabels | object | `{}` | Add custom `labels` to the Crossplane pod deployment. |
| customAnnotations | object | `{}` | Add custom `annotations` to the Crossplane pod deployment. |
| serviceAccount.customAnnotations | object | `{}` | Add custom `annotations` to the Crossplane ServiceAccount. |
| leaderElection | bool | `true` | Enable [leader election](https://docs.crossplane.io/latest/concepts/pods/#leader-election) for the Crossplane pod. |
| args | list | `[]` | Add custom arguments to the Crossplane pod. |
| provider.packages | list | `[]` | A list of Provider packages to install. |
| configuration.packages | list | `[]` | A list of Configuration packages to install. |
| function.packages | list | `[]` | A list of Function packages to install |
| imagePullSecrets | list | `["private-registry"]` | The imagePullSecret names to add to the Crossplane ServiceAccount. imagePullSecrets: [] |
| registryCaBundleConfig.name | string | `""` | The ConfigMap name containing a custom CA bundle to enable fetching packages from registries with unknown or untrusted certificates. |
| registryCaBundleConfig.key | string | `""` | The ConfigMap key containing a custom CA bundle to enable fetching packages from registries with unknown or untrusted certificates. |
| service.customAnnotations | object | `{}` | Configure annotations on the service object. Only enabled when webhooks.enabled = true |
| webhooks.enabled | bool | `true` | Enable webhooks for Crossplane and installed Provider packages. |
| rbacManager.deploy | bool | `true` | Deploy the RBAC Manager pod and its required roles. |
| rbacManager.skipAggregatedClusterRoles | bool | `false` | Don't install aggregated Crossplane ClusterRoles. |
| rbacManager.replicas | int | `1` | The number of RBAC Manager pod `replicas` to deploy. |
| rbacManager.revisionHistoryLimit | string | `nil` | The number of RBAC Manager ReplicaSets to retain. |
| rbacManager.leaderElection | bool | `true` | Enable [leader election](https://docs.crossplane.io/latest/concepts/pods/#leader-election) for the RBAC Manager pod. |
| rbacManager.args | list | `[]` | Add custom arguments to the RBAC Manager pod. |
| rbacManager.nodeSelector | object | `{}` | Add `nodeSelectors` to the RBAC Manager pod deployment. |
| rbacManager.tolerations | list | `[]` | Add `tolerations` to the RBAC Manager pod deployment. |
| rbacManager.affinity | object | `{}` | Add `affinities` to the RBAC Manager pod deployment. |
| rbacManager.topologySpreadConstraints | list | `[]` | Add `topologySpreadConstraints` to the RBAC Manager pod deployment. |
| priorityClassName | string | `""` | The PriorityClass name to apply to the Crossplane and RBAC Manager pods. |
| resourcesCrossplane.limits.cpu | string | `"500m"` | CPU resource limits for the Crossplane pod. |
| resourcesCrossplane.limits.memory | string | `"1024Mi"` | Memory resource limits for the Crossplane pod. |
| resourcesCrossplane.requests.cpu | string | `"100m"` | CPU resource requests for the Crossplane pod. |
| resourcesCrossplane.requests.memory | string | `"256Mi"` | Memory resource requests for the Crossplane pod. |
| securityContextCrossplane.runAsUser | int | `65532` | The user ID used by the Crossplane pod. |
| securityContextCrossplane.runAsGroup | int | `65532` | The group ID used by the Crossplane pod. |
| securityContextCrossplane.allowPrivilegeEscalation | bool | `false` | Enable `allowPrivilegeEscalation` for the Crossplane pod. |
| securityContextCrossplane.readOnlyRootFilesystem | bool | `true` | Set the Crossplane pod root file system as read-only. |
| packageCache.medium | string | `""` | Set to `Memory` to hold the package cache in a RAM backed file system. Useful for Crossplane development. |
| packageCache.sizeLimit | string | `"20Mi"` | The size limit for the package cache. If medium is `Memory` the `sizeLimit` can't exceed Node memory. |
| packageCache.pvc | string | `""` | The name of a PersistentVolumeClaim to use as the package cache. Disables the default package cache `emptyDir` Volume. |
| packageCache.configMap | string | `""` | The name of a ConfigMap to use as the package cache. Disables the default package cache `emptyDir` Volume. |
| resourcesRBACManager.limits.cpu | string | `"100m"` | CPU resource limits for the RBAC Manager pod. |
| resourcesRBACManager.limits.memory | string | `"512Mi"` | Memory resource limits for the RBAC Manager pod. |
| resourcesRBACManager.requests.cpu | string | `"100m"` | CPU resource requests for the RBAC Manager pod. |
| resourcesRBACManager.requests.memory | string | `"256Mi"` | Memory resource requests for the RBAC Manager pod. |
| securityContextRBACManager.runAsUser | int | `65532` | The user ID used by the RBAC Manager pod. |
| securityContextRBACManager.runAsGroup | int | `65532` | The group ID used by the RBAC Manager pod. |
| securityContextRBACManager.allowPrivilegeEscalation | bool | `false` | Enable `allowPrivilegeEscalation` for the RBAC Manager pod. |
| securityContextRBACManager.readOnlyRootFilesystem | bool | `true` | Set the RBAC Manager pod root file system as read-only. |
| metrics.enabled | bool | `false` | Enable Prometheus path, port and scrape annotations and expose port 8080 for both the Crossplane and RBAC Manager pods. |
| extraEnvVarsCrossplane | object | `{}` | Add custom environmental variables to the Crossplane pod deployment. Replaces any `.` in a variable name with `_`. For example, `SAMPLE.KEY=value1` becomes `SAMPLE_KEY=value1`. |
| extraEnvVarsRBACManager | object | `{}` | Add custom environmental variables to the RBAC Manager pod deployment. Replaces any `.` in a variable name with `_`. For example, `SAMPLE.KEY=value1` becomes `SAMPLE_KEY=value1`. |
| podSecurityContextCrossplane | object | `{}` | Add a custom `securityContext` to the Crossplane pod. |
| podSecurityContextRBACManager | object | `{}` | Add a custom `securityContext` to the RBAC Manager pod. |
| extraVolumesCrossplane | object | `{}` | Add custom `volumes` to the Crossplane pod. |
| extraVolumeMountsCrossplane | object | `{}` | Add custom `volumeMounts` to the Crossplane pod. |
| extraObjects | list | `[]` | To add arbitrary Kubernetes Objects during a Helm Install |
| istio.enabled | bool | `false` | Toggle istio integration |
| istio.mtls | object | `{"mode":"STRICT"}` | Default Crossplane peer authentication |
| istio.mtls.mode | string | `"STRICT"` | STRICT = Allow only mutual TLS traffic, PERMISSIVE = Allow both plain text and mutual TLS traffic |
| networkPolicies.enabled | bool | `false` | Toggle network policies |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.

---

_This file is programatically generated using `helm-docs` and some BigBang-specific templates. The `gluon` repository has [instructions for regenerating package READMEs](https://repo1.dso.mil/big-bang/product/packages/gluon/-/blob/master/docs/bb-package-readme.md)._

