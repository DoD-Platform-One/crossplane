# crossplane

![Version: 1.11.3-bb.0](https://img.shields.io/badge/Version-1.11.3--bb.0-informational?style=flat-square) ![AppVersion: 1.11.3](https://img.shields.io/badge/AppVersion-1.11.3-informational?style=flat-square)

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
| replicas | int | `1` |  |
| deploymentStrategy | string | `"RollingUpdate"` |  |
| image.repository | string | `"registry1.dso.mil/ironbank/opensource/crossplane/crossplane"` |  |
| image.tag | string | `"v1.11.3"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| nodeSelector | object | `{}` |  |
| tolerations | list | `[]` |  |
| affinity | object | `{}` |  |
| customLabels | object | `{}` | Custom labels to add into metadata |
| customAnnotations | object | `{}` | Custom annotations to add to the Crossplane deployment and pod |
| serviceAccount | object | `{"customAnnotations":{}}` | Custom annotations to add to the serviceaccount of Crossplane |
| leaderElection | bool | `true` |  |
| args | object | `{}` |  |
| provider.packages | list | `[]` |  |
| configuration.packages | list | `[]` |  |
| imagePullSecrets[0] | string | `"private-registry"` |  |
| registryCaBundleConfig | object | `{}` |  |
| webhooks.enabled | bool | `false` |  |
| rbacManager.deploy | bool | `true` |  |
| rbacManager.skipAggregatedClusterRoles | bool | `false` |  |
| rbacManager.replicas | int | `1` |  |
| rbacManager.managementPolicy | string | `"All"` |  |
| rbacManager.leaderElection | bool | `true` |  |
| rbacManager.args | object | `{}` |  |
| rbacManager.nodeSelector | object | `{}` |  |
| rbacManager.tolerations | list | `[]` |  |
| rbacManager.affinity | object | `{}` |  |
| priorityClassName | string | `""` |  |
| resourcesCrossplane.limits.cpu | string | `"100m"` |  |
| resourcesCrossplane.limits.memory | string | `"512Mi"` |  |
| resourcesCrossplane.requests.cpu | string | `"100m"` |  |
| resourcesCrossplane.requests.memory | string | `"256Mi"` |  |
| securityContextCrossplane.runAsUser | int | `65532` |  |
| securityContextCrossplane.runAsGroup | int | `65532` |  |
| securityContextCrossplane.allowPrivilegeEscalation | bool | `false` |  |
| securityContextCrossplane.readOnlyRootFilesystem | bool | `true` |  |
| packageCache.medium | string | `""` |  |
| packageCache.sizeLimit | string | `"5Mi"` |  |
| packageCache.pvc | string | `""` |  |
| packageCache.configMap | string | `""` |  |
| resourcesRBACManager.limits.cpu | string | `"100m"` |  |
| resourcesRBACManager.limits.memory | string | `"512Mi"` |  |
| resourcesRBACManager.requests.cpu | string | `"100m"` |  |
| resourcesRBACManager.requests.memory | string | `"256Mi"` |  |
| securityContextRBACManager.runAsUser | int | `65532` |  |
| securityContextRBACManager.runAsGroup | int | `65532` |  |
| securityContextRBACManager.allowPrivilegeEscalation | bool | `false` |  |
| securityContextRBACManager.readOnlyRootFilesystem | bool | `true` |  |
| metrics.enabled | bool | `false` |  |
| extraEnvVarsCrossplane | object | `{}` |  |
| extraEnvVarsRBACManager | object | `{}` |  |
| podSecurityContextCrossplane | object | `{}` |  |
| podSecurityContextRBACManager | object | `{}` |  |
| xfn.enabled | bool | `false` |  |
| xfn.image.repository | string | `"crossplane/xfn"` |  |
| xfn.image.tag | string | `"v1.11.3"` |  |
| xfn.image.pullPolicy | string | `"IfNotPresent"` |  |
| xfn.args | object | `{}` |  |
| xfn.extraEnvVars | object | `{}` |  |
| xfn.securityContext.runAsUser | int | `65532` |  |
| xfn.securityContext.runAsGroup | int | `65532` |  |
| xfn.securityContext.allowPrivilegeEscalation | bool | `false` |  |
| xfn.securityContext.readOnlyRootFilesystem | bool | `true` |  |
| xfn.securityContext.capabilities.add[0] | string | `"SETUID"` |  |
| xfn.securityContext.capabilities.add[1] | string | `"SETGID"` |  |
| xfn.securityContext.seccompProfile.type | string | `"Unconfined"` |  |
| xfn.cache.medium | string | `""` |  |
| xfn.cache.sizeLimit | string | `"1Gi"` |  |
| xfn.cache.pvc | string | `""` |  |
| xfn.cache.configMap | string | `""` |  |
| xfn.resources.limits.cpu | string | `"2000m"` |  |
| xfn.resources.limits.memory | string | `"2Gi"` |  |
| xfn.resources.requests.cpu | string | `"1000m"` |  |
| xfn.resources.requests.memory | string | `"1Gi"` |  |
| istio.enabled | bool | `false` |  |
| istio.mtls | object | `{"mode":"STRICT"}` | Default Crossplane peer authentication |
| istio.mtls.mode | string | `"STRICT"` | STRICT = Allow only mutual TLS traffic, PERMISSIVE = Allow both plain text and mutual TLS traffic |
| networkPolicies.enabled | bool | `false` |  |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
