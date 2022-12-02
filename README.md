# multi-k8s-crdb

A helm chart to span a cockroachdb instance across k8s clusters

## Attribution

This chart is based heavily on the official [CockroachDB chart](https://github.com/cockroachdb/helm-charts/tree/master/cockroachdb). This chart is meant to include additional templates Equinix Metal relies on.

## Memory allocation

This chart sets `max-sql-memory` and `cache` to 1GB, which is 25% of the resource memory limit. If you change the memory limit, you can adjust those two parameters accordingly.

## A note on upgrades

When doing a major version upgrade, you need to be on the latest minor version before that, e.g. to upgrade to `v22.1` you need to be running `v21.2.x`. In addition, to prevent the cluster from automatically finalizing when all the cluster nodes are upgraded to the new major version, you should set this before you start the upgrade:

```
SET CLUSTER SETTING cluster.preserve_downgrade_option = '21.2'
```

It will allow you to downgrade the cluster if you run into any issues. You can run in this state for a few days and if everything looks good, finalize the upgrade:

```
RESET CLUSTER SETTING cluster.preserve_downgrade_option
```

For more information about upgrades, see https://www.cockroachlabs.com/docs/stable/upgrade-cockroachdb-kubernetes.html

## Breaking changes

* This chart does not support the Cockroach Labs self signer.
* This chart assumes there will be externally routable pod endpoints, with dns provided by [ExternalDNS](https://github.com/kubernetes-sigs/external-dns)
* Assumes the use of [Stakater's Reloader](https://github.com/stakater/Reloader) for cert rotation.
