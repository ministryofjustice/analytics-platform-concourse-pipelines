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

### [`dev/cpanel.yaml`](dev/cpanel.yaml)
```sh
fly -t default set-pipeline -p cpanel-api -c dev/cpanel.yaml
```
A pipeline for deploying the Control Panel API to the dev cluster.

### [`dev/cpfrontend.yaml`](dev/cpfrontend.yaml)
```sh
fly -t default set-pipeline -p cpanel-frontend -c dev/cpfrontend.yaml -v cpanel-api-url=http://cpanel-master-cpanel
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

### [`alpha/cpanel.yaml`](alpha/cpanel.yaml)
```sh
fly -t default set-pipeline -p cpanel-api -c alpha/cpanel.yaml
```
A pipeline for deploying the Control Panel API to the alpha cluster.

### [`alpha/cpfrontend.yaml`](alpha/cpfrontend.yaml)
```sh
fly -t default set-pipeline -p cpanel-frontend -c alpha/cpfrontend.yaml -v cpanel-api-url=http://cpanel-master-cpanel
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
