# Concourse pipelines for components of the Analytical Platform

## Usage

These pipeline configuration files are designed to be used with Concourse to
deploy components of the MOJ Analytical Platform.

Setting a pipeline in Concourse is done using the [`fly` CLI tool](https://concourse-ci.org/fly.html)

### Teams

We currently have two Concourse team:
- `admin` with the pipelines to release Control Panel, update Helm repository, and update webapp pipelines from GH repositories
- `main` with the pipelines to release users' webapps and the `airflow` pipeline

### fly login

Example invocations of `fly` are listed alongside the documentation of each
pipeline below. You will need to `fly login` to a Concourse server before you
can set a pipeline, and on first login, you will name the "target", which is
referred to as `default` in the examples. Eg:

Most of these pipelines are in the `admin` team, so an example
login command would look like:

```sh
fly login -c https://concourse.services.alpha.mojanalytics.xyz -t alpha-admin -n admin
```

However, `airflow` pipeline is in `main` team so you'll have to login passing `-n main`:

```sh
fly login -c https://concourse.services.alpha.mojanalytics.xyz -t alpha-main -n main
```

**NOTE**: You can find the Concourse URL by getting its Kubernetes `Ingress` resource:

```sh
kubectl -n default get ingress -lapp=concourse-web
```

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
fly -t alpha-admin set-pipeline -p cpanel-api -c dev/cpanel-api.yaml
```
A pipeline for deploying the Control Panel API to the dev cluster.


### [`alpha/cpanel-api.yaml`](alpha/cpanel-api.yaml)
```sh
fly -t alpha-admin set-pipeline -p cpanel-api -c alpha/cpanel-api.yaml
```
A pipeline for deploying the Control Panel API to the alpha cluster.

### [`update-helm-repo.yaml`](alpha/update-helm-repo.yaml)
```sh
fly -t alpha-admin set-pipeline -p update-helm-repo -c alpha/update-helm-repo.yaml -v s3-bucket=moj-analytics-helm-repo -v aws-region=eu-west-1
```
A pipeline to keep our Helm repository up-to-date.
<table>
<thead><tr><th>Value</th><th>Description</th></tr></thead>
<tbody>
    <tr>
    <td><code>s3-bucket</code></td>
    <td>The name of the S3 bucket where the Helm chart packages and index YAML file are stored. Usually <code>moj-analytics-helm-repo</code>.</td></tr>
    <tr>
    <td><code>aws-region</code></td>
    <td>The AWS region where the S3 bucket is hosted. This is usually <code>eu-west-1</code>.</td></tr>
</tbody>
</table>


### [`airflow.yaml`](airflow.yaml)
NB The Data Engineering team are responsible for this pipeline

```sh
fly -t alpha-main set-pipeline -p airflow -c airflow.yaml -v repo=moj-analytical-services/airflow-dags
```
A pipeline to lint user contributed airflow DAGs in the environment specific
repo.
<table>
<thead><tr><th>Value</th><th>Description</th></tr></thead>
<tbody>
    <tr>
    <td><code>repo</code></td>
    <td>the url to the DAGs repo in the format owner/reponame/ usually
    <code>moj-analytical-services/airflow-dags</code>.</td></tr>
</tbody>
</table>

**NOTE**: This pipeline is in the `main` team so you'll have to login in that team to update it, see ["fly login" section](#fly-login).
