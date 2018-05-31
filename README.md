# analytics-platform-concourse-pipelines
Concourse pipelines for components of the Analytical Platform

## Usage

Set/update a pipeline with `fly -t target set-pipeline -p pipeline-name -f pipeline.yaml`

Eg:
```sh
fly -t default set-pipeline -p cpanel-api -f cpanel.yaml -v env=dev
```

## Values

Values can be passed to `fly` to interpolate into the pipeline YAML before
setting the pipeline config in Concourse. These values are marked in the YAML as
`((value-name))`. If a value is not passed on the `fly` command line, the value
will be [looked up in the Kubernetes secrets in the Concourse team's
namespace](https://github.com/kubernetes/charts/tree/master/stable/concourse#kubernetes-secrets)

## Pipelines

The following pipeline configs are provided in this repo:

### [`dev/cpanel.yaml`](dev/cpanel.yaml)
A pipeline for deploying the Control Panel API to the dev cluster.

### [`dev/cpfrontend.yaml`](dev/cpfrontend.yaml)
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
A pipeline for deploying the Control Panel API to the alpha cluster.

### [`alpha/cpfrontend.yaml`](alpha/cpfrontend.yaml)
A pipeline for deploying the Control Panel frontend to the alpha cluster.
<table>
<thead><tr><th>Value</th><th>Description</th></tr></thead>
<tbody>
    <tr>
    <td><code>cpanel-api-url</code></td>
    <td>The URL for the Control Panel API that the frontend will connect to. This should be <code>http://cpanel-master-cpanel/</code>, unless you are doing something unusual</td></tr>
</tbody>
</table>
