# Integrations

## Kubernetes 

Manage all Kubernetes logs and events using our easy to deploy [public helm chart](https://github.com/siglens/helm-chart).

This helm chart includes a fluentd daemonset to automatically ingest Kubernetes logs into the SigLens instance.

## FluentD

SigLens implements the nessecary ES APIs for the FluentD Elasticsearch plugin. In order to use FluentD, make sure that the `path` configuration is set to `/elastic`

Example FlunetD configuration:
```
<match siglens>
  @type elasticsearch
  host localhost
  port 8081
  path /elastic
  <buffer>
    flush_mode interval
    flush_interval 10s
    retry_forever true
  </buffer>
</match>

```

## Vector

Similar to FluentD, SigLens is compatible with the Elastic plugin for vector. Make sure that the `endpoint` has the `/elasitc` suffix.

An example sink configuration:
```
[sinks.siglens]
inputs = [ "parse_logs" ]
type = "elasticsearch"
endpoint = "http://localhost:8081/elastic"
mode = "bulk"
bulk.index = "vector-test"
```
