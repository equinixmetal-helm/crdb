# multi-k8s-crdb
A helm chart to span a cockroachdb instance across k8s clusters

## Attribution

This chart is based heavily on the official [CockroachDB chart](https://github.com/cockroachdb/helm-charts/tree/master/cockroachdb). This chart is meant to include additional templates Equinix Metal relies on.

## Breaking changes

* This chart does not support the Cockroach Labs self signer.
* This chart assumes there will be externally routable pod endpoints, with dns provided by [ExternalDNS](https://github.com/kubernetes-sigs/external-dns)
* Assumes the use of [Stakater's Reloader](https://github.com/stakater/Reloader) for cert rotation.
