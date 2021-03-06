# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2018-08-02
### Added
Added `airflow.yaml` pipeline which triggers for
PRs into the [example dags
repo](https://github.com/ministryofjustice/analytics-platform-airflow-example-dags)
in `dev` and the [airflow dags
repo](https://github.com/moj-analytical-services/airflow-dags/) in `alpha`.

## [0.1.1] - 2018-06-04
### Changed
Changed secret names to match admin-team Helm chart: secrets names must be
lowercase alphanumeric, '-' or '.'

## [0.1.0] - 2018-06-01
### Added
Added `update-helm-repo` pipeline, to keep our Helm repository up to date. This
pipeline is triggered by commits to the master branch of the
`ministryofjustice/analaytics-platform-helm-charts` Github repository and
replaces a Circle CI script which committed updated packages back to that
repository on commits.
