# loki

![Version: 2.5.1-bb.3](https://img.shields.io/badge/Version-2.5.1--bb.3-informational?style=flat-square) ![AppVersion: v2.3.0](https://img.shields.io/badge/AppVersion-v2.3.0-informational?style=flat-square)

Loki: like Prometheus, but for logs.

## Upstream References
* <https://grafana.com/loki>

* <https://github.com/grafana/loki>

## Learn More
* [Application Overview](docs/overview.md)
* [Other Documentation](docs/)

## Pre-Requisites

* Kubernetes Cluster deployed
* Kubernetes config installed in `~/.kube/config`
* Helm installed

Kubernetes: `^1.10.0-0`

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

* Clone down the repository
* cd into directory
```bash
helm install loki chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| domain | string | `"bigbang.dev"` |  |
| istio.enabled | bool | `false` |  |
| istio.loki.gateways[0] | string | `"istio-system/main"` |  |
| istio.loki.hosts[0] | string | `"loki.{{ .Values.domain }}"` |  |
| monitoring.enabled | bool | `false` |  |
| networkPolicies.enabled | bool | `false` |  |
| networkPolicies.controlPlaneCidr | string | `"0.0.0.0/0"` |  |
| monolith.enabled | bool | `true` |  |
| monolith.image.repository | string | `"registry1.dso.mil/ironbank/opensource/grafana/grafana-loki"` |  |
| monolith.image.tag | string | `"2.3.0"` |  |
| monolith.image.pullPolicy | string | `"IfNotPresent"` |  |
| monolith.image.pullSecrets[0] | string | `"private-registry"` |  |
| monolith.annotations.istioVersion | string | `nil` |  |
| scalable.enabled | bool | `false` |  |
| scalable.loki.image.registry | string | `"registry1.dso.mil"` |  |
| scalable.loki.image.repository | string | `"ironbank/opensource/grafana/grafana-loki"` |  |
| scalable.loki.image.tag | string | `"2.3.0"` |  |
| scalable.loki.image.pullPolicy | string | `"IfNotPresent"` |  |
| scalable.loki.image.pullSecrets[0] | string | `"private-registry"` |  |
| global.image.registry | string | `"registry1.dso.mil"` |  |
| global.image.repository | string | `"ironbank/opensource/grafana/grafana-loki"` |  |
| global.image.tag | string | `"2.3.0"` |  |
| global.image.pullPolicy | string | `"IfNotPresent"` |  |
| global.image.pullSecrets[0] | string | `"private-registry"` |  |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
# loki

![Version: 2.8.5](https://img.shields.io/badge/Version-2.8.5-informational?style=flat-square) ![AppVersion: v2.4.1](https://img.shields.io/badge/AppVersion-v2.4.1-informational?style=flat-square)

Loki: like Prometheus, but for logs.

## Upstream References
* <https://grafana.com/loki>

* <https://github.com/grafana/loki>

## Learn More
* [Application Overview](docs/overview.md)
* [Other Documentation](docs/)

## Pre-Requisites

* Kubernetes Cluster deployed
* Kubernetes config installed in `~/.kube/config`
* Helm installed

Kubernetes: `^1.10.0-0`

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

* Clone down the repository
* cd into directory
```bash
helm install loki chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.repository | string | `"grafana/loki"` |  |
| image.tag | string | `"2.4.1"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| ingress.enabled | bool | `false` |  |
| ingress.annotations | object | `{}` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| affinity | object | `{}` |  |
| annotations | object | `{}` |  |
| tracing.jaegerAgentHost | string | `nil` |  |
| config.auth_enabled | bool | `false` |  |
| config.ingester.chunk_idle_period | string | `"3m"` |  |
| config.ingester.chunk_block_size | int | `262144` |  |
| config.ingester.chunk_retain_period | string | `"1m"` |  |
| config.ingester.max_transfer_retries | int | `0` |  |
| config.ingester.wal.dir | string | `"/data/loki/wal"` |  |
| config.ingester.lifecycler.ring.kvstore.store | string | `"inmemory"` |  |
| config.ingester.lifecycler.ring.replication_factor | int | `1` |  |
| config.limits_config.enforce_metric_name | bool | `false` |  |
| config.limits_config.reject_old_samples | bool | `true` |  |
| config.limits_config.reject_old_samples_max_age | string | `"168h"` |  |
| config.schema_config.configs[0].from | string | `"2020-10-24"` |  |
| config.schema_config.configs[0].store | string | `"boltdb-shipper"` |  |
| config.schema_config.configs[0].object_store | string | `"filesystem"` |  |
| config.schema_config.configs[0].schema | string | `"v11"` |  |
| config.schema_config.configs[0].index.prefix | string | `"index_"` |  |
| config.schema_config.configs[0].index.period | string | `"24h"` |  |
| config.server.http_listen_port | int | `3100` |  |
| config.storage_config.boltdb_shipper.active_index_directory | string | `"/data/loki/boltdb-shipper-active"` |  |
| config.storage_config.boltdb_shipper.cache_location | string | `"/data/loki/boltdb-shipper-cache"` |  |
| config.storage_config.boltdb_shipper.cache_ttl | string | `"24h"` |  |
| config.storage_config.boltdb_shipper.shared_store | string | `"filesystem"` |  |
| config.storage_config.filesystem.directory | string | `"/data/loki/chunks"` |  |
| config.chunk_store_config.max_look_back_period | string | `"0s"` |  |
| config.table_manager.retention_deletes_enabled | bool | `false` |  |
| config.table_manager.retention_period | string | `"0s"` |  |
| config.compactor.working_directory | string | `"/data/loki/boltdb-shipper-compactor"` |  |
| config.compactor.shared_store | string | `"filesystem"` |  |
| extraArgs | object | `{}` |  |
| livenessProbe.httpGet.path | string | `"/ready"` |  |
| livenessProbe.httpGet.port | string | `"http-metrics"` |  |
| livenessProbe.initialDelaySeconds | int | `45` |  |
| networkPolicy.enabled | bool | `false` |  |
| client | object | `{}` |  |
| nodeSelector | object | `{}` |  |
| persistence.enabled | bool | `false` |  |
| persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| persistence.size | string | `"10Gi"` |  |
| persistence.annotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podAnnotations."prometheus.io/scrape" | string | `"true"` |  |
| podAnnotations."prometheus.io/port" | string | `"http-metrics"` |  |
| podManagementPolicy | string | `"OrderedReady"` |  |
| rbac.create | bool | `true` |  |
| rbac.pspEnabled | bool | `true` |  |
| readinessProbe.httpGet.path | string | `"/ready"` |  |
| readinessProbe.httpGet.port | string | `"http-metrics"` |  |
| readinessProbe.initialDelaySeconds | int | `45` |  |
| replicas | int | `1` |  |
| resources | object | `{}` |  |
| securityContext.fsGroup | int | `10001` |  |
| securityContext.runAsGroup | int | `10001` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `10001` |  |
| service.type | string | `"ClusterIP"` |  |
| service.nodePort | string | `nil` |  |
| service.port | int | `3100` |  |
| service.annotations | object | `{}` |  |
| service.labels | object | `{}` |  |
| service.targetPort | string | `"http-metrics"` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `nil` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `true` |  |
| terminationGracePeriodSeconds | int | `4800` |  |
| tolerations | list | `[]` |  |
| podDisruptionBudget | object | `{}` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |
| serviceMonitor.enabled | bool | `false` |  |
| serviceMonitor.interval | string | `""` |  |
| serviceMonitor.additionalLabels | object | `{}` |  |
| serviceMonitor.annotations | object | `{}` |  |
| initContainers | list | `[]` |  |
| extraContainers | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| extraVolumeMounts | list | `[]` |  |
| extraPorts | list | `[]` |  |
| env | list | `[]` |  |
| alerting_groups | list | `[]` |  |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
# loki-simple-scalable

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2.4.1](https://img.shields.io/badge/AppVersion-2.4.1-informational?style=flat-square)

Helm chart for Grafana Loki in simple, scalable mode

## Upstream References
* <https://grafana.github.io/helm-charts>

* <https://github.com/grafana/loki>
* <https://grafana.com/oss/loki/>
* <https://grafana.com/docs/loki/latest/>

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
helm install loki-simple-scalable chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| global.image.registry | string | `nil` | Overrides the Docker registry globally for all images |
| global.priorityClassName | string | `nil` | Overrides the priorityClassName for all pods |
| global.clusterDomain | string | `"cluster.local"` | configures cluster domain ("cluster.local" by default) |
| global.dnsService | string | `"kube-dns"` | configures DNS service name |
| global.dnsNamespace | string | `"kube-system"` | configures DNS service namespace |
| nameOverride | string | `nil` | Overrides the chart's name |
| fullnameOverride | string | `nil` | Overrides the chart's computed fullname |
| imagePullSecrets | list | `[]` | Image pull secrets for Docker images |
| loki.readinessProbe.httpGet.path | string | `"/ready"` |  |
| loki.readinessProbe.httpGet.port | string | `"http"` |  |
| loki.readinessProbe.initialDelaySeconds | int | `30` |  |
| loki.readinessProbe.timeoutSeconds | int | `1` |  |
| loki.image.registry | string | `"docker.io"` | The Docker registry |
| loki.image.repository | string | `"grafana/loki"` | Docker image repository |
| loki.image.tag | string | `nil` | Overrides the image tag whose default is the chart's appVersion |
| loki.image.pullPolicy | string | `"IfNotPresent"` | Docker image pull policy |
| loki.podAnnotations | object | `{}` | Common annotations for all pods |
| loki.revisionHistoryLimit | int | `10` | The number of old ReplicaSets to retain to allow rollback |
| loki.podSecurityContext | object | `{"fsGroup":10001,"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001}` | The SecurityContext for Loki pods |
| loki.containerSecurityContext | object | `{"allowPrivilegeEscalation":false,"capabilities":{"drop":["ALL"]},"readOnlyRootFilesystem":true}` | The SecurityContext for Loki containers |
| loki.existingSecretForConfig | string | `""` | Specify an existing secret containing loki configuration. If non-empty, overrides `loki.config` |
| loki.config | object | See values.yaml | Config file contents for Loki |
| loki.storageConfig | object | loki.defaultStorageConfig | Common storage config component of loki configuration file. The must be overriden with a valid object storage backend in order for queries to work. |
| loki.defaultStorageConfig | object | `{"filesystem":{"chunks_directory":"/var/loki/chunks,","rules_directory":"/var/loki/rules"}}` | Default storage config, used when no loki.storageConfig is provided. Required for CI, but queries will not work using these defaults. |
| serviceAccount.create | bool | `true` | Specifies whether a ServiceAccount should be created |
| serviceAccount.name | string | `nil` | The name of the ServiceAccount to use. If not set and create is true, a name is generated using the fullname template |
| serviceAccount.imagePullSecrets | list | `[]` | Image pull secrets for the service account |
| serviceAccount.annotations | object | `{}` | Annotations for the service account |
| serviceAccount.automountServiceAccountToken | bool | `true` | Set this toggle to false to opt out of automounting API credentials for the service account |
| rbac.pspEnabled | bool | `false` | If enabled, a PodSecurityPolicy is created |
| serviceMonitor.enabled | bool | `false` | If enabled, ServiceMonitor resources for Prometheus Operator are created |
| serviceMonitor.namespace | string | `nil` | Alternative namespace for ServiceMonitor resources |
| serviceMonitor.namespaceSelector | object | `{}` | Namespace selector for ServiceMonitor resources |
| serviceMonitor.annotations | object | `{}` | ServiceMonitor annotations |
| serviceMonitor.labels | object | `{}` | Additional ServiceMonitor labels |
| serviceMonitor.interval | string | `nil` | ServiceMonitor scrape interval |
| serviceMonitor.scrapeTimeout | string | `nil` | ServiceMonitor scrape timeout in Go duration format (e.g. 15s) |
| serviceMonitor.relabelings | list | `[]` | ServiceMonitor relabel configs to apply to samples before scraping https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/api.md#relabelconfig |
| serviceMonitor.scheme | string | `"http"` | ServiceMonitor will use http by default, but you can pick https as well |
| serviceMonitor.tlsConfig | string | `nil` | ServiceMonitor will use these tlsConfig settings to make the health check requests |
| prometheusRule.enabled | bool | `false` | If enabled, a PrometheusRule resource for Prometheus Operator is created |
| prometheusRule.namespace | string | `nil` | Alternative namespace for the PrometheusRule resource |
| prometheusRule.annotations | object | `{}` | PrometheusRule annotations |
| prometheusRule.labels | object | `{}` | Additional PrometheusRule labels |
| prometheusRule.groups | list | `[]` | Contents of Prometheus rules file |
| write.replicas | int | `1` | Number of replicas for the write |
| write.image.registry | string | `nil` | The Docker registry for the write image. Overrides `loki.image.registry` |
| write.image.repository | string | `nil` | Docker image repository for the write image. Overrides `loki.image.repository` |
| write.image.tag | string | `nil` | Docker image tag for the write image. Overrides `loki.image.tag` |
| write.priorityClassName | string | `nil` | The name of the PriorityClass for write pods |
| write.podAnnotations | object | `{}` | Annotations for write pods |
| write.serviceLabels | object | `{}` | Labels for ingestor service |
| write.extraArgs | list | `[]` | Additional CLI args for the write |
| write.extraEnv | list | `[]` | Environment variables to add to the write pods |
| write.extraEnvFrom | list | `[]` | Environment variables from secrets or configmaps to add to the write pods |
| write.extraVolumeMounts | list | `[]` | Volume mounts to add to the write pods |
| write.extraVolumes | list | `[]` | Volumes to add to the write pods |
| write.resources | object | `{}` | Resource requests and limits for the write |
| write.terminationGracePeriodSeconds | int | `300` | Grace period to allow the write to shutdown before it is killed. Especially for the ingestor, this must be increased. It must be long enough so writes can be gracefully shutdown flushing/transferring all data and to successfully leave the member ring on shutdown. |
| write.affinity | string | Hard node and soft zone anti-affinity | Affinity for write pods. Passed through `tpl` and, thus, to be configured as string |
| write.nodeSelector | object | `{}` | Node selector for write pods |
| write.tolerations | list | `[]` | Tolerations for write pods |
| write.persistence.size | string | `"10Gi"` | Size of persistent disk |
| write.persistence.storageClass | string | `nil` | Storage class to be used. If defined, storageClassName: <storageClass>. If set to "-", storageClassName: "", which disables dynamic provisioning. If empty or set to null, no storageClassName spec is set, choosing the default provisioner (gp2 on AWS, standard on GKE, AWS, and OpenStack). |
| read.replicas | int | `1` | Number of replicas for the read |
| read.autoscaling.enabled | bool | `false` | Enable autoscaling for the read, this is only used if `queryIndex.enabled: true` |
| read.autoscaling.minReplicas | int | `1` | Minimum autoscaling replicas for the read |
| read.autoscaling.maxReplicas | int | `3` | Maximum autoscaling replicas for the read |
| read.autoscaling.targetCPUUtilizationPercentage | int | `60` | Target CPU utilisation percentage for the read |
| read.autoscaling.targetMemoryUtilizationPercentage | string | `nil` | Target memory utilisation percentage for the read |
| read.image.registry | string | `nil` | The Docker registry for the read image. Overrides `loki.image.registry` |
| read.image.repository | string | `nil` | Docker image repository for the read image. Overrides `loki.image.repository` |
| read.image.tag | string | `nil` | Docker image tag for the read image. Overrides `loki.image.tag` |
| read.priorityClassName | string | `nil` | The name of the PriorityClass for read pods |
| read.podAnnotations | object | `{}` | Annotations for read pods |
| read.serviceLabels | object | `{}` | Labels for read service |
| read.extraArgs | list | `[]` | Additional CLI args for the read |
| read.extraEnv | list | `[]` | Environment variables to add to the read pods |
| read.extraEnvFrom | list | `[]` | Environment variables from secrets or configmaps to add to the read pods |
| read.extraVolumeMounts | list | `[]` | Volume mounts to add to the read pods |
| read.extraVolumes | list | `[]` | Volumes to add to the read pods |
| read.resources | object | `{}` | Resource requests and limits for the read |
| read.terminationGracePeriodSeconds | int | `30` | Grace period to allow the read to shutdown before it is killed |
| read.affinity | string | Hard node and soft zone anti-affinity | Affinity for read pods. Passed through `tpl` and, thus, to be configured as string |
| read.nodeSelector | object | `{}` | Node selector for read pods |
| read.tolerations | list | `[]` | Tolerations for read pods |
| read.persistence.size | string | `"10Gi"` | Size of persistent disk |
| read.persistence.storageClass | string | `nil` | Storage class to be used. If defined, storageClassName: <storageClass>. If set to "-", storageClassName: "", which disables dynamic provisioning. If empty or set to null, no storageClassName spec is set, choosing the default provisioner (gp2 on AWS, standard on GKE, AWS, and OpenStack). |
| gateway.enabled | bool | `true` | Specifies whether the gateway should be enabled |
| gateway.replicas | int | `1` | Number of replicas for the gateway |
| gateway.verboseLogging | bool | `true` | Enable logging of 2xx and 3xx HTTP requests |
| gateway.autoscaling.enabled | bool | `false` | Enable autoscaling for the gateway |
| gateway.autoscaling.minReplicas | int | `1` | Minimum autoscaling replicas for the gateway |
| gateway.autoscaling.maxReplicas | int | `3` | Maximum autoscaling replicas for the gateway |
| gateway.autoscaling.targetCPUUtilizationPercentage | int | `60` | Target CPU utilisation percentage for the gateway |
| gateway.autoscaling.targetMemoryUtilizationPercentage | string | `nil` | Target memory utilisation percentage for the gateway |
| gateway.deploymentStrategy | object | `{"type":"RollingUpdate"}` | See `kubectl explain deployment.spec.strategy` for more -- ref: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#strategy |
| gateway.image.registry | string | `"docker.io"` | The Docker registry for the gateway image |
| gateway.image.repository | string | `"nginxinc/nginx-unprivileged"` | The gateway image repository |
| gateway.image.tag | string | `"1.19-alpine"` | The gateway image tag |
| gateway.image.pullPolicy | string | `"IfNotPresent"` | The gateway image pull policy |
| gateway.priorityClassName | string | `nil` | The name of the PriorityClass for gateway pods |
| gateway.podAnnotations | object | `{}` | Annotations for gateway pods |
| gateway.extraArgs | list | `[]` | Additional CLI args for the gateway |
| gateway.extraEnv | list | `[]` | Environment variables to add to the gateway pods |
| gateway.extraEnvFrom | list | `[]` | Environment variables from secrets or configmaps to add to the gateway pods |
| gateway.extraVolumes | list | `[]` | Volumes to add to the gateway pods |
| gateway.extraVolumeMounts | list | `[]` | Volume mounts to add to the gateway pods |
| gateway.podSecurityContext | object | `{"fsGroup":101,"runAsGroup":101,"runAsNonRoot":true,"runAsUser":101}` | The SecurityContext for gateway containers |
| gateway.containerSecurityContext | object | `{"allowPrivilegeEscalation":false,"capabilities":{"drop":["ALL"]},"readOnlyRootFilesystem":true}` | The SecurityContext for gateway containers |
| gateway.resources | object | `{}` | Resource requests and limits for the gateway |
| gateway.terminationGracePeriodSeconds | int | `30` | Grace period to allow the gateway to shutdown before it is killed |
| gateway.affinity | string | Hard node and soft zone anti-affinity | Affinity for gateway pods. Passed through `tpl` and, thus, to be configured as string |
| gateway.nodeSelector | object | `{}` | Node selector for gateway pods |
| gateway.tolerations | list | `[]` | Tolerations for gateway pods |
| gateway.service.port | int | `80` | Port of the gateway service |
| gateway.service.type | string | `"ClusterIP"` | Type of the gateway service |
| gateway.service.clusterIP | string | `nil` | ClusterIP of the gateway service |
| gateway.service.nodePort | string | `nil` | Node port if service type is NodePort |
| gateway.service.loadBalancerIP | string | `nil` | Load balancer IPO address if service type is LoadBalancer |
| gateway.service.annotations | object | `{}` | Annotations for the gateway service |
| gateway.service.labels | object | `{}` | Labels for gateway service |
| gateway.ingress.enabled | bool | `false` | Specifies whether an ingress for the gateway should be created |
| gateway.ingress.annotations | object | `{}` | Ingress Class Name. MAY be required for Kubernetes versions >= 1.18 ingressClassName: nginx -- Annotations for the gateway ingress |
| gateway.ingress.hosts | list | `[{"host":"gateway.loki.example.com","paths":[{"path":"/"}]}]` | Hosts configuration for the gateway ingress |
| gateway.ingress.tls | list | `[{"hosts":["gateway.loki.example.com"],"secretName":"loki-gateway-tls"}]` | TLS configuration for the gateway ingress |
| gateway.basicAuth.enabled | bool | `false` | Enables basic authentication for the gateway |
| gateway.basicAuth.username | string | `nil` | The basic auth username for the gateway |
| gateway.basicAuth.password | string | `nil` | The basic auth password for the gateway |
| gateway.basicAuth.htpasswd | string | `"{{ htpasswd (required \"'gateway.basicAuth.username' is required\" .Values.gateway.basicAuth.username) (required \"'gateway.basicAuth.password' is required\" .Values.gateway.basicAuth.password) }}"` | Uses the specified username and password to compute a htpasswd using Sprig's `htpasswd` function. The value is templated using `tpl`. Override this to use a custom htpasswd, e.g. in case the default causes high CPU load. |
| gateway.basicAuth.existingSecret | string | `nil` | Existing basic auth secret to use. Must contain '.htpasswd' |
| gateway.readinessProbe.httpGet.path | string | `"/"` |  |
| gateway.readinessProbe.httpGet.port | string | `"http"` |  |
| gateway.readinessProbe.initialDelaySeconds | int | `15` |  |
| gateway.readinessProbe.timeoutSeconds | int | `1` |  |
| gateway.nginxConfig.logFormat | string | `"main '$remote_addr - $remote_user [$time_local]  $status '\n        '\"$request\" $body_bytes_sent \"$http_referer\" '\n        '\"$http_user_agent\" \"$http_x_forwarded_for\"';"` | NGINX log format |
| gateway.nginxConfig.serverSnippet | string | `""` | Allows appending custom configuration to the server block |
| gateway.nginxConfig.httpSnippet | string | `""` | Allows appending custom configuration to the http block |
| gateway.nginxConfig.file | string | See values.yaml | Config file contents for Nginx. Passed through the `tpl` function to allow templating |
| networkPolicy.enabled | bool | `false` | Specifies whether Network Policies should be created |
| networkPolicy.metrics.podSelector | object | `{}` | Specifies the Pods which are allowed to access the metrics port. As this is cross-namespace communication, you also need the namespaceSelector. |
| networkPolicy.metrics.namespaceSelector | object | `{}` | Specifies the namespaces which are allowed to access the metrics port |
| networkPolicy.metrics.cidrs | list | `[]` | Specifies specific network CIDRs which are allowed to access the metrics port. In case you use namespaceSelector, you also have to specify your kubelet networks here. The metrics ports are also used for probes. |
| networkPolicy.ingress.podSelector | object | `{}` | Specifies the Pods which are allowed to access the http port. As this is cross-namespace communication, you also need the namespaceSelector. |
| networkPolicy.ingress.namespaceSelector | object | `{}` | Specifies the namespaces which are allowed to access the http port |
| networkPolicy.alertmanager.port | int | `9093` | Specify the alertmanager port used for alerting |
| networkPolicy.alertmanager.podSelector | object | `{}` | Specifies the alertmanager Pods. As this is cross-namespace communication, you also need the namespaceSelector. |
| networkPolicy.alertmanager.namespaceSelector | object | `{}` | Specifies the namespace the alertmanager is running in |
| networkPolicy.externalStorage.ports | list | `[]` | Specify the port used for external storage, e.g. AWS S3 |
| networkPolicy.externalStorage.cidrs | list | `[]` | Specifies specific network CIDRs you want to limit access to |
| networkPolicy.discovery.port | string | `nil` | Specify the port used for discovery |
| networkPolicy.discovery.podSelector | object | `{}` | Specifies the Pods labels used for discovery. As this is cross-namespace communication, you also need the namespaceSelector. |
| networkPolicy.discovery.namespaceSelector | object | `{}` | Specifies the namespace the discovery Pods are running in |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
# loki

![Version: 2.5.1-bb.2](https://img.shields.io/badge/Version-2.5.1--bb.2-informational?style=flat-square) ![AppVersion: v2.3.0](https://img.shields.io/badge/AppVersion-v2.3.0-informational?style=flat-square)

Loki: like Prometheus, but for logs.

## Upstream References
* <https://grafana.com/loki>

* <https://github.com/grafana/loki>

## Learn More
* [Application Overview](docs/overview.md)
* [Other Documentation](docs/)

## Pre-Requisites

* Kubernetes Cluster deployed
* Kubernetes config installed in `~/.kube/config`
* Helm installed

Kubernetes: `^1.10.0-0`

Install Helm

https://helm.sh/docs/intro/install/

## Deployment

* Clone down the repository
* cd into directory
```bash
helm install loki chart/
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.repository | string | `"registry1.dso.mil/ironbank/opensource/grafana/grafana-loki"` |  |
| image.tag | string | `"2.3.0"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.pullSecrets[0] | string | `"private-registry"` |  |
| ingress.enabled | bool | `false` |  |
| ingress.annotations | object | `{}` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| imagePullSecrets | object | `{}` |  |
| affinity | object | `{}` |  |
| annotations | object | `{}` |  |
| tracing.jaegerAgentHost | string | `nil` |  |
| config.auth_enabled | bool | `false` |  |
| config.ingester.chunk_idle_period | string | `"3m"` |  |
| config.ingester.chunk_block_size | int | `262144` |  |
| config.ingester.chunk_retain_period | string | `"1m"` |  |
| config.ingester.max_transfer_retries | int | `0` |  |
| config.ingester.lifecycler.ring.kvstore.store | string | `"inmemory"` |  |
| config.ingester.lifecycler.ring.replication_factor | int | `1` |  |
| config.limits_config.enforce_metric_name | bool | `false` |  |
| config.limits_config.reject_old_samples | bool | `true` |  |
| config.limits_config.reject_old_samples_max_age | string | `"168h"` |  |
| config.schema_config.configs[0].from | string | `"2020-10-24"` |  |
| config.schema_config.configs[0].store | string | `"boltdb-shipper"` |  |
| config.schema_config.configs[0].object_store | string | `"filesystem"` |  |
| config.schema_config.configs[0].schema | string | `"v11"` |  |
| config.schema_config.configs[0].index.prefix | string | `"index_"` |  |
| config.schema_config.configs[0].index.period | string | `"24h"` |  |
| config.server.http_listen_port | int | `3100` |  |
| config.storage_config.boltdb_shipper.active_index_directory | string | `"/data/loki/boltdb-shipper-active"` |  |
| config.storage_config.boltdb_shipper.cache_location | string | `"/data/loki/boltdb-shipper-cache"` |  |
| config.storage_config.boltdb_shipper.cache_ttl | string | `"24h"` |  |
| config.storage_config.boltdb_shipper.shared_store | string | `"filesystem"` |  |
| config.storage_config.filesystem.directory | string | `"/data/loki/chunks"` |  |
| config.chunk_store_config.max_look_back_period | string | `"0s"` |  |
| config.table_manager.retention_deletes_enabled | bool | `false` |  |
| config.table_manager.retention_period | string | `"0s"` |  |
| config.compactor.working_directory | string | `"/data/loki/boltdb-shipper-compactor"` |  |
| config.compactor.shared_store | string | `"filesystem"` |  |
| extraArgs | object | `{}` |  |
| livenessProbe.httpGet.path | string | `"/ready"` |  |
| livenessProbe.httpGet.port | string | `"http-metrics"` |  |
| livenessProbe.initialDelaySeconds | int | `45` |  |
| networkPolicy.enabled | bool | `false` |  |
| networkPolicies.enabled | bool | `false` |  |
| networkPolicies.controlPlaneCidr | string | `"0.0.0.0/0"` |  |
| monitoring.enabled | bool | `false` |  |
| client | object | `{}` |  |
| nodeSelector | object | `{}` |  |
| persistence.enabled | bool | `false` |  |
| persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| persistence.size | string | `"10Gi"` |  |
| persistence.annotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podAnnotations."prometheus.io/scrape" | string | `"true"` |  |
| podAnnotations."prometheus.io/port" | string | `"http-metrics"` |  |
| podManagementPolicy | string | `"OrderedReady"` |  |
| rbac.create | bool | `true` |  |
| rbac.pspEnabled | bool | `true` |  |
| readinessProbe.httpGet.path | string | `"/ready"` |  |
| readinessProbe.httpGet.port | string | `"http-metrics"` |  |
| readinessProbe.initialDelaySeconds | int | `45` |  |
| replicas | int | `1` |  |
| resources.limits.cpu | string | `"250m"` |  |
| resources.limits.memory | string | `"256Mi"` |  |
| resources.requests.cpu | string | `"250m"` |  |
| resources.requests.memory | string | `"256Mi"` |  |
| securityContext.fsGroup | int | `10001` |  |
| securityContext.runAsGroup | int | `10001` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `10001` |  |
| service.type | string | `"ClusterIP"` |  |
| service.nodePort | string | `nil` |  |
| service.port | int | `3100` |  |
| service.annotations | object | `{}` |  |
| service.labels | object | `{}` |  |
| service.targetPort | string | `"http-metrics"` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `nil` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `true` |  |
| terminationGracePeriodSeconds | int | `4800` |  |
| tolerations | list | `[]` |  |
| podDisruptionBudget | object | `{}` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |
| serviceMonitor.enabled | bool | `false` |  |
| serviceMonitor.interval | string | `""` |  |
| serviceMonitor.additionalLabels | object | `{}` |  |
| serviceMonitor.annotations | object | `{}` |  |
| initContainers | list | `[]` |  |
| extraContainers | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| extraVolumeMounts | list | `[]` |  |
| extraPorts | list | `[]` |  |
| env | list | `[]` |  |
| alerting_groups | list | `[]` |  |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
