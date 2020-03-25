## TL;DR

based on https://github.com/helm/charts/tree/master/stable/verdaccio with adding initContainer to fix NFS gid issue.

## CHANGES

* templates/deployment.yaml: add initContainer to fix EFS mount permission.
* values.yaml: add `persistence.useFsgroupInitContainer: BOOL` to control initContainer.
