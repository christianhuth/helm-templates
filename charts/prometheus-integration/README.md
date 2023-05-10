# Scope

These examples don't show how to create a metrics endpoint in your application. It assumes that your Application already exposes metrics on a port called http-metrics, like this:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: <POD_NAME>
spec:
    containers:
    - name: <CONTAINER_NAME>
        image: <IMAGE_REGISTRY>/<IMAGE_REPOSITORY>:<IMAGE:TAG>
        ports:
        - name: http-metrics
            containerPort: {{ .Values.metrics.service.port }}
            protocol: TCP
```

> **IMPORTANT:** Make sure to set the default value of `metrics.service.port` to your specific port used to expose your metrics.

## Content

The examples consist of [Named Templates](./templates/_helpers.tpl), that are used in Templates for the following resources:

- [PodMonitor](./templates/metrics/podmonitor.yaml)
- [PrometheusRule](./templates/metrics/prometheusrule.yaml)
- [Service](./templates/metrics/service.yaml)
- [ServiceMonitor](./templates/metrics/servicemonitor.yaml)

> **IMPORTANT:** Rename the Named Templates from `mychart.` to the name of your Helm chart.

## See created resources

To see the created resources, run the following command:

```
helm template -f values.yaml --set metrics.enabled=true .
```

By default no PodMonitor will be created as this is usually not needed. To see this resource as well run:

```
helm template -f values.yaml --set metrics.enabled=true --set metrics.podmonitor.enabled=true .
```

## Read my Blog article about the concepts behind these Templates

https://blog.knell.it/making-your-helm-chart-observable-by-prometheus

## Provided values

## Values

| Key                                      | Type   | Default                                                                                     | Description                                                                                |
| ---------------------------------------- | ------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| metrics.enabled                          | bool   | `false`                                                                                     | enable the Prometheus                                                                      |
| metrics.podMonitor.additionalLabels      | object | `{}`                                                                                        | Additional labels that can be used so ServiceMonitor will be discovered by Prometheus      |
| metrics.podMonitor.enabled               | bool   | `false`                                                                                     | Create PodMonitor Resource for scraping metrics using Prometheus Operator                  |
| metrics.podMonitor.honorLabels           | bool   | `false`                                                                                     | Specify honorLabels parameter to add the scrape endpoint                                   |
| metrics.podMonitor.interval              | string | `"30s"`                                                                                     | Interval at which metrics should be scraped.                                               |
| metrics.podMonitor.jobLabel              | string | `""`                                                                                        | The name of the label on the target service to use as the job name in Prometheus           |
| metrics.podMonitor.metricRelabelings     | object | `{}`                                                                                        | MetricRelabelConfigs to apply to samples before ingestion                                  |
| metrics.podMonitor.namespace             | string | `""`                                                                                        | Namespace for the ServiceMonitor Resource (defaults to the Release Namespace)              |
| metrics.podMonitor.relabelings           | object | `{}`                                                                                        | RelabelConfigs to apply to samples before scraping                                         |
| metrics.podMonitor.scrapeTimeout         | string | `""`                                                                                        | Timeout after which the scrape is ended                                                    |
| metrics.podMonitor.selector              | object | `{}`                                                                                        | Prometheus instance selector labels                                                        |
| metrics.prometheusRule.additionalLabels  | object | `{}`                                                                                        | Additional labels that can be used so PrometheusRule will be discovered by Prometheus      |
| metrics.prometheusRule.enabled           | bool   | `false`                                                                                     | Create a PrometheusRule for Prometheus Operator                                            |
| metrics.prometheusRule.namespace         | string | `""`                                                                                        | Namespace for the PrometheusRule Resource (defaults to the Release Namespace)              |
| metrics.prometheusRule.rules             | list   | `[]`                                                                                        | PrometheusRule definitions                                                                 |
| metrics.service.annotations              | object | `{"prometheus.io/port":"{{ .Values.metrics.service.port }}","prometheus.io/scrape":"true"}` | Annotations for Prometheus to auto-discover the metrics endpoint                           |
| metrics.service.port                     | int    | `9095`                                                                                      | Prometheus Exporter service port                                                           |
| metrics.service.sessionAffinity          | string | `"None"`                                                                                    | Control where client requests go, to the same pod or round-robin. Values: ClientIP or None |
| metrics.serviceMonitor.additionalLabels  | object | `{}`                                                                                        | Additional labels that can be used so ServiceMonitor will be discovered by Prometheus      |
| metrics.serviceMonitor.enabled           | bool   | `true`                                                                                      | Create ServiceMonitor Resource for scraping metrics using Prometheus Operator              |
| metrics.serviceMonitor.honorLabels       | bool   | `false`                                                                                     | Specify honorLabels parameter to add the scrape endpoint                                   |
| metrics.serviceMonitor.interval          | string | `"30s"`                                                                                     | Interval at which metrics should be scraped.                                               |
| metrics.serviceMonitor.jobLabel          | string | `""`                                                                                        | The name of the label on the target service to use as the job name in Prometheus           |
| metrics.serviceMonitor.metricRelabelings | object | `{}`                                                                                        | MetricRelabelConfigs to apply to samples before ingestion                                  |
| metrics.serviceMonitor.namespace         | string | `""`                                                                                        | Namespace for the ServiceMonitor Resource (defaults to the Release Namespace)              |
| metrics.serviceMonitor.relabelings       | object | `{}`                                                                                        | RelabelConfigs to apply to samples before scraping                                         |
| metrics.serviceMonitor.scrapeTimeout     | string | `""`                                                                                        | Timeout after which the scrape is ended                                                    |
| metrics.serviceMonitor.selector          | object | `{}`                                                                                        | Prometheus instance selector labels                                                        |

---

Autogenerated from chart metadata using [helm-docs v1.11.0](https://github.com/norwoodj/helm-docs/releases/v1.11.0)
