# SigLens

SigLens is an Open Source Observability solution that is **100x** more efficient than Splunk, Elastic. 

# Why SigLens:
Our experience servicing 10,000+ engineers with Observability tools taught us a few things:

- Developers have to jump through different tools for logs, metrics, traces
- Splunk, DataDog, NewRelic are very expensive
- ElasticSearch takes too many machines, cluster maintainence is hard
- Grafana Loki has slow query performance

Armed with decades of experience in monitoring domain, we set out to build a observability DB from the ground up, uniquely suited for logs, metrics and traces with **`zero`** external dependency. A **`single binary`** that you can run on your laptop and process `8 TB/day` on it.  
<br /><br />


## Join our Slack community

Come say Hi to us on [Slack](www.siglens.com/slack) 👋

<br /><br />

## Getting Started

### Using SigLens Binary
`go run cmd/siglens/main.go --config server.yaml`

### Using SigLens Docker
`TBD`

# Features:

1. Multiple Ingestion formats: Open Telemetry, Elastic, Splunk HEC, Loki
2. Multiple Query Languages: Splunk SPL, SQL and Loki LogQL
3. Simple architecture, easy to get started.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) to get started with making contributions to SigLens.

