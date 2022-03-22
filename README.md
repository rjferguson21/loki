# loki

![Version: 3.0.0-bb.0](https://img.shields.io/badge/Version-3.0.0--bb.0-informational?style=flat-square) ![AppVersion: v2.4.2](https://img.shields.io/badge/AppVersion-v2.4.2-informational?style=flat-square)

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
| global.image.priorityClassName | string | `nil` |  |
| global.image.pullPolicy | string | `"IfNotPresent"` |  |
| global.image.pullSecrets[0] | string | `"private-registry"` |  |
| domain | string | `"bigbang.dev"` |  |
| istio.enabled | bool | `false` |  |
| istio.loki.gateways[0] | string | `"istio-system/main"` |  |
| istio.loki.hosts[0] | string | `"loki.{{ .Values.domain }}"` |  |
| monitoring.enabled | bool | `false` |  |
| networkPolicies.enabled | bool | `false` |  |
| networkPolicies.controlPlaneCidr | string | `"0.0.0.0/0"` |  |
| loki.enabled | bool | `true` |  |
| loki.image.repository | string | `"registry1.dso.mil/ironbank/opensource/grafana/loki"` |  |
| loki.image.tag | string | `"2.4.2"` |  |
| loki.image.pullPolicy | string | `"IfNotPresent"` |  |
| loki.image.pullSecrets[0] | string | `"private-registry"` |  |
| loki-simple-scalable.enabled | bool | `false` |  |
| loki-simple-scalable.image.registry | string | `"registry1.dso.mil"` | The Docker registry |
| loki-simple-scalable.image.repository | string | `"ironbank/opensource/grafana/loki"` | Docker image repository |
| loki-simple-scalable.image.tag | string | `"2.4.2"` | Overrides the image tag whose default is the chart's appVersion |
| loki-simple-scalable.image.pullPolicy | string | `"IfNotPresent"` | Docker image pull policy |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `nil` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `true` |  |
| minio.enabled | bool | `true` |  |
| minio.accessKey | string | `"enterprise-logs"` |  |
| minio.secretKey | string | `"supersecret"` |  |
| minio.buckets[0].name | string | `"enterprise-logs-tsdb"` |  |
| minio.buckets[0].policy | string | `"none"` |  |
| minio.buckets[0].purge | bool | `false` |  |
| minio.buckets[1].name | string | `"enterprise-logs-admin"` |  |
| minio.buckets[1].policy | string | `"none"` |  |
| minio.buckets[1].purge | bool | `false` |  |
| minio.buckets[2].name | string | `"enterprise-logs-ruler"` |  |
| minio.buckets[2].policy | string | `"none"` |  |
| minio.buckets[2].purge | bool | `false` |  |
| minio.persistence.size | string | `"5Gi"` |  |
| minio.resources.requests.cpu | string | `"100m"` |  |
| minio.resources.requests.memory | string | `"128Mi"` |  |
| gel.enabled | bool | `false` |  |
| gel.nameOverride | string | `nil` | Overrides the chart's name |
| gel.fullnameOverride | string | `nil` | Overrides the chart's computed fullname |
| gel.image | object | `{"pullPolicy":"IfNotPresent","pullSecrets":[],"registry":"docker.io","repository":"grafana/enterprise-logs","tag":"v1.3.0"}` | Definition of the Docker image for Grafana Enterprise Logs If the image block is overwritten in a custom values file, it is also required to update the values in the `loki-distributed.loki.image` block. This can be done by copying the values, or like here, by using an anchor and a pointer. |
| gel.image.registry | string | `"docker.io"` | The container registry to use |
| gel.image.repository | string | `"grafana/enterprise-logs"` | The image repository to use |
| gel.image.tag | string | `"v1.3.0"` | The version of Grafana Enterprise Logs |
| gel.image.pullPolicy | string | `"IfNotPresent"` | Defines the policy how and when images are pulled |
| gel.image.pullSecrets | list | `[]` | Additional image pull secrets |
| gel.serviceAccount | object | `{"create":true}` | Definition of the ServiceAccount for containers Any additional configuration of the ServiceAccount has to be done in `loki-distributed.serviceAccount`. |
| gel.serviceAccount.create | bool | `true` | Specifies whether a ServiceAccount should be created If this value is changed to `false`, it also needs to be reflected in `loki-distributed.serviceAccount.create`. |
| gel.useExternalConfig | bool | `false` | External config.yaml A GEL configuration file may be provided as Kubernetes Secret outside of this Helm chart. |
| gel.externalConfigName | string | `"enterprise-logs-config"` |  |
| gel.externalConfigVersion | string | `"0"` |  |
| gel.useExternalLicense | bool | `false` | External license.jwt A GEL license file may be provided as Kubernetes Secret outside of this Helm chart. |
| gel.externalLicenseName | string | `"enterprise-logs-license"` |  |
| gel.externalLicenseVersion | string | `"0"` |  |
| gel.license | object | `{"cluster_name":null,"contents":"NOTAVALIDLICENSE"}` | Grafana Enterprise Logs license In order to use Grafana Enterprise Logs features, you will need to provide the contents of your Grafana Enterprise Logs license, either by providing the contents of the license.jwt, or the name Kubernetes Secret that contains your license.jwt. To set the license contents, use the flag `--set-file 'license.contents=./license.jwt'` |
| gel.config | string | `"auth:\n  type: enterprise\nauth_enabled: true\n\nlicense:\n  path: \"/etc/enterprise-logs/license/license.jwt\"\n\ncluster_name: {{ .Release.Name }}\n\nserver:\n  http_listen_port: 3100\n  grpc_listen_port: 9095\n\ncommon:\n  replication_factor: 1\n  storage:\n    filesystem: null\n    s3:\n      endpoint: {{ include \"enterprise-logs.minio\" . }}\n      secret_access_key: supersecret\n      access_key_id: enterprise-logs\n      insecure: true\n      s3forcepathstyle: true\n\nmemberlist:\n  join_members:\n    - {{ include \"loki.fullname\" . }}-memberlist-tcp\n\nadmin_client:\n  storage:\n    type: s3\n    s3:\n      bucket_name: enterprise-logs-admin\n\ncompactor:\n  shared_store: s3\n  working_directory: /var/loki/boltdb-shipper-compactor\n  compaction_interval: 30s\n\ningester:\n  lifecycler:\n    num_tokens: 512\n  chunk_idle_period: 30m\n  chunk_block_size: 262144\n  chunk_encoding: snappy\n  chunk_retain_period: 1m\n  wal:\n    dir: /var/loki/wal\n\ningester_client:\n  grpc_client_config:\n    max_recv_msg_size: 104857600\n    max_send_msg_size: 104857600\n\nlimits_config:\n  enforce_metric_name: false\n  reject_old_samples: true\n  reject_old_samples_max_age: 168h\n  max_cache_freshness_per_query: 10m\n\nfrontend:\n  log_queries_longer_than: 10s\n  compress_responses: true\n  tail_proxy_url: http://{{ include \"loki.fullname\" . }}:3100\n\nquerier:\n  query_ingesters_within: 12h\n\nquery_range:\n  split_queries_by_interval: 24h\n  align_queries_with_step: true\n  cache_results: true\n  results_cache:\n    cache:\n      memcached:\n        expiration: 1h\n      memcached_client:\n        timeout: 1s\n\nschema_config:\n  configs:\n    - from: 2021-01-01\n      store: boltdb-shipper\n      object_store: aws\n      schema: v11\n      index:\n        prefix: index_\n        period: 24h\n\nstorage_config:\n  aws:\n    endpoint: {{ include \"enterprise-logs.minio\" . }}\n    bucketnames: enterprise-logs-tsdb\n    access_key_id: enterprise-logs\n    secret_access_key: supersecret\n    s3forcepathstyle: true\n    insecure: true\n  boltdb_shipper:\n    active_index_directory: /var/loki/index\n    cache_location: /var/loki/cache\n    cache_ttl: 24h\n    shared_store: s3\n\nruler:\n  storage:\n    type: s3\n    s3:\n      bucketnames: enterprise-logs-ruler\n  enable_alertmanager_discovery: false\n  enable_api: true\n  enable_sharding: true\n  rule_path: /var/loki\n"` | Grafana Enterprise Logs configuration file |
| gel.tokengen | object | `{"annotations":{},"enable":true,"env":[],"extraArgs":{},"extraVolumeMounts":[],"extraVolumes":[],"labels":{},"priorityClassName":null,"securityContext":{"fsGroup":10001,"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001}}` | Configuration for `tokengen` target |
| gel.tokengen.enable | bool | `true` | Whether the job should be part of the deployment |
| gel.tokengen.extraArgs | object | `{}` | Additional CLI arguments for the `tokengen` target |
| gel.tokengen.env | list | `[]` | Additional Kubernetes environment |
| gel.tokengen.labels | object | `{}` | Additional labels for the `tokengen` Job |
| gel.tokengen.annotations | object | `{}` | Additional annotations for the `tokengen` Job |
| gel.tokengen.extraVolumes | list | `[]` | Additional volumes for Pods |
| gel.tokengen.extraVolumeMounts | list | `[]` | Additional volume mounts for Pods |
| gel.tokengen.securityContext | object | `{"fsGroup":10001,"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001}` | Run containers as user `enterprise-logs(uid=10001)` |
| gel.adminApi | object | `{"affinity":{},"annotations":{},"env":[],"extraArgs":{},"extraContainers":[],"extraVolumeMounts":[],"extraVolumes":[],"initContainers":[],"labels":{},"livenessProbe":{"httpGet":{"path":"/ready","port":"http-metrics"},"initialDelaySeconds":45},"nodeSelector":{},"persistence":{"subPath":null},"readinessProbe":{"httpGet":{"path":"/ready","port":"http-metrics"},"initialDelaySeconds":45},"replicas":1,"resources":{},"securityContext":{"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001},"service":{"annotations":{},"labels":{}},"strategy":{"type":"RollingUpdate"},"terminationGracePeriodSeconds":60,"tolerations":[]}` | Configuration for the `admin-api` target |
| gel.adminApi.replicas | int | `1` | Define the amount of instances |
| gel.adminApi.extraArgs | object | `{}` | Additional CLI arguments for the `admin-api` target |
| gel.adminApi.labels | object | `{}` | Additional labels for the `admin-api` Deployment |
| gel.adminApi.annotations | object | `{}` | Additional annotations for the `admin-api` Deployment |
| gel.adminApi.service | object | `{"annotations":{},"labels":{}}` | Additional labels and annotations for the `admin-api` Service |
| gel.adminApi.securityContext | object | `{"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001}` | Run container as user `enterprise-logs(uid=10001)` `fsGroup` must not be specified, because these security options are applied on container level not on Pod level. |
| gel.adminApi.resources | object | `{}` | Request and limit Kubernetes resources -- Values are defined in small.yaml and large.yaml |
| gel.adminApi.extraVolumes | list | `[]` | Additional volumes for Pods |
| gel.adminApi.extraVolumeMounts | list | `[]` | Additional volume mounts for Pods |
| gel.adminApi.affinity | object | `{}` | Affinity for admin-api Pods |
| gel.adminApi.nodeSelector | object | `{}` | Node selector for admin-api Pods |
| gel.adminApi.tolerations | list | `[]` | Tolerations for admin-api Pods |
| gel.adminApi.terminationGracePeriodSeconds | int | `60` | Grace period to allow the admin-api to shutdown before it is killed |
| gel.gateway | object | `{"affinity":{},"annotations":{},"env":[],"extraArgs":{},"extraContainers":[],"extraVolumeMounts":[],"extraVolumes":[],"initContainers":[],"labels":{},"livenessProbe":{"httpGet":{"path":"/ready","port":"http-metrics"},"initialDelaySeconds":45},"nodeSelector":{},"persistence":{"subPath":null},"readinessProbe":{"httpGet":{"path":"/ready","port":"http-metrics"},"initialDelaySeconds":45},"replicas":1,"resources":{},"securityContext":{"fsGroup":10001,"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001},"service":{"annotations":{},"labels":{}},"strategy":{"type":"RollingUpdate"},"terminationGracePeriodSeconds":60,"tolerations":[],"useDefaultProxyURLs":true}` | Configuration for the `gateway` target |
| gel.gateway.replicas | int | `1` | Define the amount of instances |
| gel.gateway.extraArgs | object | `{}` | Additional CLI arguments for the `gateway` target |
| gel.gateway.labels | object | `{}` | Additional labels for the `gateway` Pod |
| gel.gateway.annotations | object | `{}` | Additional annotations for the `gateway` Pod |
| gel.gateway.service | object | `{"annotations":{},"labels":{}}` | Additional labels and annotations for the `gateway` Service |
| gel.gateway.securityContext | object | `{"fsGroup":10001,"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001}` | Run container as user `enterprise-logs(uid=10001)` |
| gel.gateway.resources | object | `{}` | Request and limit Kubernetes resources -- Values are defined in small.yaml and large.yaml |
| gel.gateway.extraVolumes | list | `[]` | Additional volumes for Pods |
| gel.gateway.extraVolumeMounts | list | `[]` | Additional volume mounts for Pods |
| gel.gateway.affinity | object | `{}` | Affinity for gateway Pods |
| gel.gateway.nodeSelector | object | `{}` | Node selector for gateway Pods |
| gel.gateway.tolerations | list | `[]` | Tolerations for gateway Pods |
| gel.gateway.terminationGracePeriodSeconds | int | `60` | Grace period to allow the gateway to shutdown before it is killed |
| gel.compactor | object | `{"affinity":{"podAntiAffinity":{"preferredDuringSchedulingIgnoredDuringExecution":[{"podAffinityTerm":{"labelSelector":{"matchExpressions":[{"key":"target","operator":"In","values":["compactor"]}]},"topologyKey":"kubernetes.io/hostname"},"weight":100}]}},"annotations":{},"env":[],"extraArgs":{},"extraContainers":[],"extraVolumeMounts":[],"extraVolumes":[],"initContainers":[],"labels":{},"livenessProbe":{"failureThreshold":20,"httpGet":{"path":"/ready","port":"http-metrics","scheme":"HTTP"},"initialDelaySeconds":180,"periodSeconds":30,"successThreshold":1,"timeoutSeconds":1},"nodeSelector":{},"persistentVolume":{"accessModes":["ReadWriteOnce"],"annotations":{},"enabled":true,"size":"2Gi","subPath":""},"readinessProbe":{"httpGet":{"path":"/ready","port":"http-metrics"},"initialDelaySeconds":60},"replicas":1,"resources":{},"securityContext":{"fsGroup":10001,"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001},"service":{"annotations":{},"labels":{}},"strategy":{"type":"RollingUpdate"},"terminationGracePeriodSeconds":300,"tolerations":[]}` | Configuration for the `compactor` target |
| gel.compactor.replicas | int | `1` | Define the amount of instances |
| gel.compactor.extraArgs | object | `{}` | Additional CLI arguments for the `compactor` target |
| gel.compactor.labels | object | `{}` | Additional labels for the `compactor` Pod |
| gel.compactor.annotations | object | `{}` | Additional annotations for the `compactor` Pod |
| gel.compactor.service | object | `{"annotations":{},"labels":{}}` | Additional labels and annotations for the `compactor` Service |
| gel.compactor.securityContext | object | `{"fsGroup":10001,"runAsGroup":10001,"runAsNonRoot":true,"runAsUser":10001}` | Run containers as user `enterprise-logs(uid=10001)` |
| gel.compactor.resources | object | `{}` | Request and limit Kubernetes resources -- Values are defined in small.yaml and large.yaml |
| gel.compactor.extraVolumes | list | `[]` | Additional volumes for Pods |
| gel.compactor.extraVolumeMounts | list | `[]` | Additional volume mounts for Pods |
| gel.compactor.affinity | object | `{"podAntiAffinity":{"preferredDuringSchedulingIgnoredDuringExecution":[{"podAffinityTerm":{"labelSelector":{"matchExpressions":[{"key":"target","operator":"In","values":["compactor"]}]},"topologyKey":"kubernetes.io/hostname"},"weight":100}]}}` | Affinity for compactor Pods |
| gel.compactor.nodeSelector | object | `{}` | Node selector for compactor Pods |
| gel.compactor.tolerations | list | `[]` | Tolerations for compactor Pods |
| gel.compactor.terminationGracePeriodSeconds | int | `300` | Grace period to allow the compactor to shutdown before it is killed |

## Contributing

Please see the [contributing guide](./CONTRIBUTING.md) if you are interested in contributing.
