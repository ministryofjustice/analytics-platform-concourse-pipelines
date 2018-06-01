# analytics-platform-concourse-pipelines
Concourse pipelines for components of the Analytical Platform

## Values

Values can be passed to `fly` to interpolate into the pipeline YAML before
setting the pipeline config in Concourse. These values are marked in the YAML as
`((value-name))`. If a value is not passed on the `fly` command line, the value
will be [looked up in the Kubernetes secrets in the Concourse team's
namespace](https://github.com/kubernetes/charts/tree/master/stable/concourse#kubernetes-secrets)

## Pipelines

The following pipeline configs are provided in this repo:

### [`dev/cpanel-api.yaml`](dev/cpanel-api.yaml)
```sh
fly -t default set-pipeline -p cpanel-api -c dev/cpanel-api.yaml
```
A pipeline for deploying the Control Panel API to the dev cluster.

### [`dev/cpanel-frontend.yaml`](dev/cpanel-frontend.yaml)
```sh
fly -t default set-pipeline -p cpanel-frontend -c dev/cpanel-frontend.yaml -v cpanel-api-url=http://cpanel-master-cpanel
```
A pipeline for deploying the Control Panel frontend to the dev cluster.
<table>
<thead><tr><th>Value</th><th>Description</th></tr></thead>
<tbody>
    <tr>
    <td><code>cpanel-api-url</code></td>
    <td>The URL for the Control Panel API that the frontend will connect to. This should be <code>http://cpanel-master-cpanel/</code>, unless you are doing something unusual</td></tr>
</tbody>
</table>

### [`alpha/cpanel-api.yaml`](alpha/cpanel-api.yaml)
```sh
fly -t default set-pipeline -p cpanel-api -c alpha/cpanel-api.yaml
```
A pipeline for deploying the Control Panel API to the alpha cluster.

### [`alpha/cpanel-frontend.yaml`](alpha/cpanel-frontend.yaml)
```sh
fly -t default set-pipeline -p cpanel-frontend -c alpha/cpanel-frontend.yaml -v cpanel-api-url=http://cpanel-master-cpanel
```
A pipeline for deploying the Control Panel frontend to the alpha cluster.
<table>
<thead><tr><th>Value</th><th>Description</th></tr></thead>
<tbody>
    <tr>
    <td><code>cpanel-api-url</code></td>
    <td>The URL for the Control Panel API that the frontend will connect to. This should be <code>http://cpanel-master-cpanel/</code>, unless you are doing something unusual</td></tr>
</tbody>
</table>

### [`update-helm-repo.yaml`](update-helm-repo.yaml)
```sh
fly -t default set-pipeline -p update-helm-repo -c update-helm-repo.yaml -v s3-bucket=moj-analytics-helm-repo -v aws-region=eu-west-1
```
A pipeline to keep our Helm repository up-to-date.
<table>
<thead><tr><th>Value</th><th>Description</th></tr></thead>
<tbody>
    <tr>
    <td><code>s3-bucket</code></td>
    <td>The name of the S3 bucket where the Helm chart packages and index YAML file are stored. Usually `moj-analytics-helm-repo`.</td></tr>
    <tr>
    <td><code>aws-region</code></td>
    <td>The AWS region where the S3 bucket is hosted. This is usually `eu-west-1`.</td></tr>
</tbody>
</table>
