# Ingestion
## Load Mock Data

Quickly load mock data into SigLens using the following commands:
```bash
curl -L https://github.com/siglens/ss-pub-data/releases/download/v1.0.0/prod-data-100mb.json.tar.gz -o prod-data-100mb.json.tar.gz 
tar -xjOf prod-data-100mb.json.tar.gz > prod-data-100mb.json  
curl http://localhost:8081/elastic/_bulk -i  --data-binary "@prod-data-100mb.json"
```

For larger volumes of data, use:
```
curl -L https://github.com/siglens/ss-pub-data/releases/download/v1.0.0/prod-data-1gb.json.tar.gz -o prod-data-1gb.json
curl -L https://github.com/siglens/ss-pub-data/releases/download/v1.0.0/prod-data-4gb.json.tar.gz -o prod-data-4gb.json
```

## Elasticsearch APIs

SigLens supports a subset of ES indexing apis to allow for compatability with existing pipelines. All ES apis have a prefix of `/elastic/`

Using the Elasticsearch Bulk API at `/elastic/_bulk` is the recommended method to ingest data into SigLens. [Bulk API Reference](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html)

SigLens follows the Elasticsearch API format for ingesting single documents. Note, this means that different APIs will be available depending on the configured value of [`esVersion`](installation.md).


For esVersion >= 7.x:
```
PUT /elastic/<indexName>/_doc/<_id>
POST /elastic/<indexName>/_doc/
PUT /elastic/<indexName>/_create/<_id>
POST /elastic/<indexName>/_create/<_id>
```

For esVersion < 7.x:
```
PUT /elastic/<indexName>/<docType>/<_id>
POST /elastic/<indexName>/<docType>/
PUT /elastic/<indexName>/<docType>/<_id>/_create/
POST /elastic/<indexName>/<docType>/<_id>/_create/
```