## 2.0.5

FIXES:

* Added compression improvements on the span forwarding path to reduce wire size of requests sent from satellites to Lightstep SaaS.

* Increased COLLECTOR_SPAN_FORWARDING_BUFFER_SIZE buffer to 20,000 as the default: You no longer need to configure this parameter.

* Added days_until_key_expiry: This new satellite key expiry metric returns the days before key expires, based on the satellite_key_id. This is the ID shown on the Satellite Keys tab of the Account Settings page.

* OTLP tracing upgraded to support v0.9

* Go upgraded to v1.17

* gzip compression for OTLP/HTTP ingest: Previously, if you sent spans compressed using GZIP, they wouldn’t unzip properly and the request would fail. This has been fixed.

* Running Microsatellites as containers: Previously, if you ran satellites as containers, we incorrectly set GOMAXPROCS to the number of CPUs in the machine of the container. We now correctly read the number of CPUs allocated to the container to set GOMAXPROCS. This has incremental performance benefits.

## 2.0.4

FIXES:

* Improvements to the metric config mapping. Reduces redundant entries and fixes some ordering problems.

BREAKING CHANGES:

* Changes the metric `lightstep_bytes_received` to `lightstep_bytes action=received`. Any dashboards that use the metric `lightstep_bytes_received` 

## 2.0.3

FIXES:

* Finalized removing of the ingress configurations that weren't used

## 2.0.2

ENHANCEMENTS:

* Clean up values.yaml and README
* Improve default resource allocation
* Update metrics mappings

FIXES:
* Update default metric sidecar path to work OOTB

## 2.0.1

ENHANCEMENTS:

* Changed the defaults of service accounts for running the satellite. This wil prevent insufficient permissions errors when running the pods
* Updated the default resources to match in-line with the recommended memory usage

## 2.0.0

This repo is a fork of [lightstep-satellite-helm-chart](https://github.com/lightstep/lightstep-satellite-helm-chart/) for Lightstep microsatellites. Everything version 2.0.0 and after will be for microsatellites only.

Breaking changes:
- Point repository to [lightstep/microsatellite](https://hub.docker.com/r/lightstep/microsatellite)
- Bump version to `2021-03-22_13-16-05Z`
- Remove optional config `bytes_per_project` (deprecated with microsatellites)

## 1.2.2

BUG FIXES:

* rolebindings: fix overzealous whitespace removal in `if` directives

## 1.2.1

BUG FIXES:

* statsd-mapping configmap: fix outdated configmap name in deployment template

## 1.2.0

ENHANCEMENTS:

* lightstep/collector: update image to `2021-01-26_23-02-36Z`
* prom/statsd-exporter: update image to `v0.20.0`
* satellite config: Satellite GUID now defaults to pod name using Downward API
* service account: role, clusterRole, and corresponding bindings are now createable through the chart
* kubernetes secret and configmap names: resource names are now based on Helm release name to allow multiple installs without conflict or dependency on other install's resources
* securityContext: run user as nonroot with UID 1000

BUG FIXES:

* nodeSelector: deployment template properly renders if object defined for `nodeSelector`
* affinity: deployment template properly renders if object defined for `affinity`
* tolerations: deployment template properly renders if object defined for `tolerations`
* securityContext: remove `drop: ["ALL"]` for capabilities

BREAKING CHANGES:

* satellite secret: secret name now uses the helm release name
* statsd-mapping configmap: configmap name now uses the helm release name
* securityContext: run user as nonroot with UID 1000
