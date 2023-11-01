# SigLens

SigLens is an open-source observability platform that is 100x faster than the existing tools. SigLens can be used to ingest, store, and query metrics,logs and traces at scale.

## Features:

1. Ingest data in various formats such as Elastic, OTEL, Splunk HEC, Loki Ingestion format
2. Support for different query languages Splunk SPL, SQL and Loki LogQL
3. UI Compatibility with Grafana Dashboards/UI, Superset UI, Any SQL client/UIs
4. Simple architecture and easy to get started.

## Getting Started

### Start Siglens
`go run cmd/siglens/main.go --config server.yaml`

#### Synthetic Data

Use [sigclient](https://github.com/siglens/sigscalr-client) to send synthetic data:
```
go run main.go ingest esbulk -t 10_000 -d http://localhost:8081/elastic --processCount 1 -n 1 -b 500 -g dynamic-user
```

Test Queries:
```
go run main.go query esbulk -d http://localhost:80/elastic -n 10 -v
```

Get started in minutes with: [Binary, Helm, Or Docker](installation.md)

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) to get started with making contributions to SigLens.

