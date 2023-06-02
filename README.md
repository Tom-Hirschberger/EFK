# Changes

Changes needed to get the EFK tutorial to work

## ElasticSearch

* Only Kubernetes 1.25 or 1.26 available; ElasticSearch 7.9.0 not compatible with both of them
* Running version 8.X costs to mouch resources and caused the pods to restart periodically. Needed to go back to 7.X
* First with Kubernetes 1.25 or 1.26 compatible version is 7.17.X
* `helm install elasticsearch elastic/elasticsearch --version="7.17.3" -f values-linode.yaml`

## Kibana

* Same as with ElasticSearch
* Current 8.X Kibana requires authentication
* `helm install kibana elastic/kibana --version="7.17.3"`

## Fluentd

* `helm install fluentd bitnami/fluentd --version="2.0.1"` does not work
* Lowest Chart Version 5.1.11 with fluentd 1.14.6 or current Chart Version 5.8.2 with fluentd 1.16.1 available in repo
* fluentd-forwarder-cm is now splitted to fluentd-inputs.conf, fluentd-output.conf, fluentd.conf, metrics.conf
* "format json" not working.
* The elastic client of fluentd 1.16.1 is not compatible with ElasticSearch 7.17.3 neither is fluentd 1.14.6
* As of [https://github.com/bitnami/charts/issues/10539](https://github.com/bitnami/charts/issues/10539)
  * `helm repo add bitnami-pre-2022 https://raw.githubusercontent.com/bitnami/charts/eb5f9a9513d987b519f0ecd732e7031241c50328/bitnami`
  * `helm install fluentd bitnami-pre-2022/fluentd --version="2.0.1"`
