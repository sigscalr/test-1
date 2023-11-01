## SigLens Installation

<!-- tabs:start -->

### Helm / K8s

SigLens provides a easy to deploy helm chart that includes a fluentd daemonset that automatically ingests kubernetes logs.

```bash
helm repo add siglens-helm https://siglens.github.io/helm-chart
helm upgrade --install siglens siglens-helm/siglens
```

Details for helm values can be found in our [public helm chart repository](https://github.com/siglens/helm-chart)

###  Docker 

The SigLens backend is deployed independently of the UI. 
To allow the UI to connect to the backend a docker network can be used.
```bash
wget https://siglens-configs.s3.amazonaws.com/1.1.31/server.yaml
docker pull public.ecr.aws/l3t9n5v5/siglens:1.1.31
mkdir data
docker run -it --mount type=bind,source="$(pwd)"/data,target=/siglens/data \
    --mount type=bind,source="$(pwd)"/server.yaml,target=/siglens/server.yaml \
    -p 8081:8081 -p 80:80 public.ecr.aws/l3t9n5v5/siglens:1.1.31
```
To be able to query data across restarts, set `ssInstanceName` in server.yaml.

The target for the data directory mounting should be the same as the data directory (`dataPath`configuration) in server.yaml

### **Binary**

SigLens provides a single binary for the following:
- Linux OS: os=linux, arch=arm64/amd64
- Mac OS:  os=darwin, arch=arm64/amd64

```bash
wget https://siglens-releases.s3.amazonaws.com/siglens-1.1.31-{os}-{arch}.tar.gz
tar -xf siglens-1.1.31-{os}-{arch}.tar.gz
cd siglens-1.1.31-{os}-{arch}/
./siglens --config server.yaml
```

<!-- tabs:end -->

Get data in SigLens by [loading sample data](ingestion), using our [supported ingestion methods](ingestion), or [integrating with your existing tools](integrations).

!> Facing issues? [Join our slack (use email to signup)](www.sigscalr.io/slack)
## Configurations

Override default behavior by editing the configuration file

| Config Variable      | Description | Default | Notes |
| ----------- | ----------- | -----------  | ------ |
| port      | Port for SigLens server       | `8081` | |
| uiPort   | Port for SigLens UI server        | `8000` | If not specified, the UI server will not be started
| dataPath | Path of directory to store data to and query from | `"./data"` |
| retentionDays | Number of historical data to keep. | `90`
| timestampKey | Timestamp key to use | `"timestamp"` |
| licenseKeyPath | Path to the license key | `"./"` |
| esVersion | Version of ES / Kibana for backwards compatability | `"6.8.20"`
| memoryThresholdPercent | Maximum percent of available RAM that SigLens will try to use | `80`
| baseLogDir | Directory to output logs to | `""` | logs to stdout if `""` |
| logFileRotationSizeMB | Size at which log rotation will be applied | `100` 
| ssInstanceName | Instance name override | `""` | For ephemeral servers (docker, k8s) set this variable to persist data across restarts
| siglensHost | Address for SigLens backend | `""` | This config is only used if SigLensUI is running independently | This address should include port, for example `localhost:8080`

## Contact Us

Any feedback or questions? Contact us at info@siglens.com





