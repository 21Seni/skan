# skan

Kubernetes manifests and rendered Helm or Kustomize resources can contain insecure settings or miss operational checks. skan scans these YAML resources against security and operations policies, then writes a report for review.

## Features

- Scan one or more Kubernetes YAML files or directories.
- Read manifests from standard input for Helm and Kustomize pipelines.
- Check workload, ingress, service, admission controller, API access, and secret-related configurations.
- Report critical, high, medium, low, and passing results.
- Write reports as HTML, YAML, or JSON.

## Installation

Download the latest release for Linux, macOS, or Windows from the [release page](https://github.com/alcideio/skan/releases/latest).

On Linux or macOS, the project also provides an install script:

```sh
curl https://raw.githubusercontent.com/alcideio/skan/master/skan-download.sh | bash
```

Verify that the `skan` executable is available on your `PATH`:

```sh
skan --help
```

## Usage

Scan a Kubernetes manifest and generate the default HTML report:

```sh
skan manifest -f mydeployment.yaml
```

The report is written to `skan-result.html`. To print passing checks and choose another output format:

```sh
skan manifest --report-passed -f mydeployment.yaml -o json --outputfile skan-result.json
```

Read rendered Helm output from standard input:

```sh
helm template kaudit deploy/charts/kaudit --set k8sAuditEnvironment=eks | skan manifest -f -
```

Read Kustomize output from standard input:

```sh
kubectl kustomize helloWorld | skan manifest -f -
```

## License

skan is licensed under the Apache License 2.0. This project is based on [alcideio/skan](https://github.com/alcideio/skan); please preserve that attribution and the applicable license notices when redistributing it.
