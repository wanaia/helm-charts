# linkerd-jaeger

The Linkerd-Jaeger extension adds distributed tracing to Linkerd using
OpenCensus and Jaeger.

![Version: 2025.7.4](https://img.shields.io/badge/Version-2025.7.4-informational?style=flat-square)

![AppVersion: edge-XX.X.X](https://img.shields.io/badge/AppVersion-edge--XX.X.X-informational?style=flat-square)

**Homepage:** <https://linkerd.io>

## Quickstart and documentation

You can run Linkerd on any Kubernetes cluster in a matter of seconds. See
the [Linkerd Getting Started Guide][getting-started] for how.

For more comprehensive documentation, start with the [Linkerd
docs][linkerd-docs].

## Prerequisite: Linkerd Core Control-Plane

Before installing the Linkerd Jaeger extension, The core control-plane has to
be installed first by following the [Linkerd Install
Guide](https://linkerd.io/2/tasks/install/).

## Adding Linkerd's Helm repository

```bash
# To add the repo for Linkerd edge releases:
helm repo add linkerd https://helm.linkerd.io/edge
```

## Installing the Jaeger Extension Chart

### Helm v3

```bash
helm install linkerd-jaeger -n linkerd-jaeger --create-namespace linkerd/linkerd-jaeger
```

## Get involved

* Check out Linkerd's source code at [GitHub][linkerd2].
* Join Linkerd's [user mailing list][linkerd-users], [developer mailing
  list][linkerd-dev], and [announcements mailing list][linkerd-announce].
* Follow [@linkerd][twitter] on Twitter.
* Join the [Linkerd Slack][slack].

[getting-started]: https://linkerd.io/2/getting-started/
[linkerd2]: https://github.com/linkerd/linkerd2
[linkerd-announce]: https://lists.cncf.io/g/cncf-linkerd-announce
[linkerd-dev]: https://lists.cncf.io/g/cncf-linkerd-dev
[linkerd-docs]: https://linkerd.io/2/overview/
[linkerd-users]: https://lists.cncf.io/g/cncf-linkerd-users
[slack]: http://slack.linkerd.io
[twitter]: https://twitter.com/linkerd

## Requirements

Kubernetes: `>=1.23.0-0`

| Repository | Name | Version |
|------------|------|---------|
| file://../../../charts/partials | partials | 0.1.0 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| clusterDomain | string | `"cluster.local"` | Kubernetes DNS Domain name to use |
| collector.GID | string | `nil` | GID for the collector resource |
| collector.UID | string | `nil` | UID for the collector resource |
| collector.command | string | `"/otelcol-contrib"` |  |
| collector.config | object | see `value.yaml` for actual configuration | OpenTelemetry Collector config, See the [Configuration docs](https://opentelemetry.io/docs/collector/configuration/) for more information |
| collector.enabled | bool | `true` | Set to false to exclude collector installation |
| collector.env | list | `[]` | Collector Deployment env |
| collector.image.name | string | `"otel/opentelemetry-collector-contrib"` |  |
| collector.image.pullPolicy | string | `""` |  |
| collector.image.version | string | `"0.83.0"` |  |
| collector.nodeSelector | object | `{"kubernetes.io/os":"linux"}` | NodeSelector section, See the [K8S documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#nodeselector) for more information |
| collector.replicas | int | `1` | Number of replicas of the collector component |
| collector.resources.cpu.limit | string | `nil` | Maximum amount of CPU units that the collector container can use |
| collector.resources.cpu.request | string | `nil` | Amount of CPU units that the collector container requests |
| collector.resources.ephemeral-storage.limit | string | `""` | Maximum amount of ephemeral storage that the collector container can use |
| collector.resources.ephemeral-storage.request | string | `""` | Amount of ephemeral storage that the collector container requests |
| collector.resources.memory.limit | string | `nil` | Maximum amount of memory that collector container can use |
| collector.resources.memory.request | string | `nil` | Amount of memory that the collector container requests |
| collector.tolerations | string | `nil` | Tolerations section, See the [K8S documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more information |
| commonLabels | object | `{}` | Labels to apply to all resources |
| createNamespaceMetadataJob | bool | `true` | Creates a Job that adds necessary metadata to the extension's namespace during install; disable if lack of privileges require doing this manually |
| defaultGID | int | `2103` | Default GID for all the jaeger components |
| defaultUID | int | `2103` | Default UID for all the jaeger components |
| enablePSP | bool | `false` | Create Roles and RoleBindings to associate this extension's ServiceAccounts to the control plane PSP resource. This requires that `enabledPSP` is set to true on the control plane install. Note PSP has been deprecated since k8s v1.21 |
| enablePodAntiAffinity | bool | `false` | Enables Pod Anti Affinity logic to balance the placement of replicas across hosts and zones for High Availability. Enable this only when you have multiple replicas of components. |
| imagePullSecrets | list | `[]` | For Private docker registries, authentication is needed.  Registry secrets are applied to the respective service accounts |
| jaeger.GID | string | `nil` | GID for the jaeger resource |
| jaeger.UID | string | `nil` | UID for the jaeger resource |
| jaeger.args | list | `["--query.base-path=/jaeger"]` | CLI arguments for Jaeger, See [Jaeger AIO Memory CLI reference](https://www.jaegertracing.io/docs/1.24/cli/#jaeger-all-in-one-memory) |
| jaeger.enabled | bool | `true` | Set to false to exclude all-in-one Jaeger installation |
| jaeger.image.name | string | `"jaegertracing/all-in-one"` |  |
| jaeger.image.pullPolicy | string | `""` |  |
| jaeger.image.version | float | `1.31` |  |
| jaeger.nodeSelector | object | `{"kubernetes.io/os":"linux"}` | NodeSelector section, See the [K8S documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#nodeselector) for more information |
| jaeger.resources.cpu.limit | string | `nil` | Maximum amount of CPU units that the jaeger container can use |
| jaeger.resources.cpu.request | string | `nil` | Amount of CPU units that the jaeger container requests |
| jaeger.resources.ephemeral-storage.limit | string | `""` | Maximum amount of ephemeral storage that the jaeger container can use |
| jaeger.resources.ephemeral-storage.request | string | `""` | Amount of ephemeral storage that the jaeger container requests |
| jaeger.resources.memory.limit | string | `nil` | Maximum amount of memory that jaeger container can use |
| jaeger.resources.memory.request | string | `nil` | Amount of memory that the jaeger container requests |
| jaeger.tolerations | string | `nil` | Tolerations section, See the [K8S documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more information |
| linkerdNamespace | string | `"linkerd"` | Namespace of the Linkerd core control-plane install |
| linkerdVersion | string | `"linkerdVersionValue"` |  |
| namespaceMetadata.image.name | string | `"extension-init"` | Docker image name for the namespace-metadata instance |
| namespaceMetadata.image.pullPolicy | string | imagePullPolicy | Pull policy for the namespace-metadata instance |
| namespaceMetadata.image.registry | string | `"cr.l5d.io/linkerd"` | Docker registry for the namespace-metadata instance |
| namespaceMetadata.image.tag | string | `"v0.1.4"` | Docker image tag for the namespace-metadata instance |
| namespaceMetadata.nodeSelector | object | `{"kubernetes.io/os":"linux"}` | NodeSelector section, See the [K8S documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#nodeselector) for more information |
| namespaceMetadata.tolerations | string | `nil` | Tolerations section, See the [K8S documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more information |
| nodeSelector | object | `{"kubernetes.io/os":"linux"}` | Default nodeSelector section, See the [K8S documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#nodeselector) for more information |
| podLabels | object | `{}` | Additional labels to add to all pods |
| revisionHistoryLimit | int | `10` | Specifies the number of old ReplicaSets to retain to allow rollback. |
| tolerations | string | `nil` | Default tolerations section, See the [K8S documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more information |
| webhook.GID | string | `nil` | GID for the webhook resource |
| webhook.UID | string | `nil` | UID for the webhook resource |
| webhook.caBundle | string | `""` | Bundle of CA certificates for webhook. If not provided nor injected with cert-manager, then Helm will use the certificate generated for `webhook.crtPEM`. If `webhook.externalSecret` is set to true, this value, injectCaFrom, or injectCaFromSecret must be set, as no certificate will be generated. See the cert-manager [CA Injector Docs](https://cert-manager.io/docs/concepts/ca-injector) for more information. |
| webhook.collectorSvcAccount | string | `"collector"` | service account associated with the collector instance |
| webhook.collectorSvcAddr | string | `"collector.linkerd-jaeger:4317"` | collector service address for the proxies to send trace data. Points by default to the linkerd-jaeger collector |
| webhook.collectorTraceProtocol | string | `"opentelemetry"` | protocol proxies should use to send trace data. Can be `opencensus` or `opentelemetry` (default) |
| webhook.collectorTraceSvcName | string | `"linkerd-proxy"` | name of the service proxies should use for exported traces |
| webhook.crtPEM | string | `""` | Certificate for the webhook. If not provided and not using an external secret then Helm will generate one. |
| webhook.externalSecret | bool | `false` | Do not create a secret resource for the webhook. If this is set to `true`, the value `webhook.caBundle` must be set or the ca bundle must injected with cert-manager ca injector using `webhook.injectCaFrom` or `webhook.injectCaFromSecret` (see below). |
| webhook.failurePolicy | string | `"Ignore"` |  |
| webhook.image.name | string | `"cr.l5d.io/linkerd/jaeger-webhook"` |  |
| webhook.image.pullPolicy | string | `""` |  |
| webhook.image.version | string | `"linkerdVersionValue"` |  |
| webhook.injectCaFrom | string | `""` | Inject the CA bundle from a cert-manager Certificate. See the cert-manager [CA Injector Docs](https://cert-manager.io/docs/concepts/ca-injector/#injecting-ca-data-from-a-certificate-resource) for more information. |
| webhook.injectCaFromSecret | string | `""` | Inject the CA bundle from a Secret. If set, the `cert-manager.io/inject-ca-from-secret` annotation will be added to the webhook. The Secret must have the CA Bundle stored in the `ca.crt` key and have the `cert-manager.io/allow-direct-injection` annotation set to `true`. See the cert-manager [CA Injector Docs](https://cert-manager.io/docs/concepts/ca-injector/#injecting-ca-data-from-a-secret-resource) for more information. |
| webhook.keyPEM | string | `""` | Certificate key for the webhook. If not provided and not using an external secret then Helm will generate one. |
| webhook.logLevel | string | `"info"` |  |
| webhook.namespaceSelector | object | `{"matchExpressions":[{"key":"kubernetes.io/metadata.name","operator":"NotIn","values":["kube-system"]}]}` | Namespace selector used by admission webhook. |
| webhook.nodeSelector | object | `{"kubernetes.io/os":"linux"}` | NodeSelector section, See the [K8S documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#nodeselector) for more information |
| webhook.objectSelector | string | `nil` |  |
| webhook.replicas | int | `1` | Number of replicas of the jaeger-injector component |
| webhook.resources.cpu.limit | string | `nil` | Maximum amount of CPU units that the jaeger-injector container can use |
| webhook.resources.cpu.request | string | `nil` | Amount of CPU units that the jaeger-injector container requests |
| webhook.resources.memory.limit | string | `nil` | Maximum amount of memory that jaeger-injector container can use |
| webhook.resources.memory.request | string | `nil` | Amount of memory that the jaeger-injector container requests |
| webhook.tolerations | string | `nil` | Tolerations section, See the [K8S documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for more information |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
