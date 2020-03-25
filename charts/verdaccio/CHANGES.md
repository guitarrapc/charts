## TL;DR

based on https://github.com/helm/charts/tree/master/stable/verdaccio with adding initContainer to fix NFS gid issue.

## CHANGES

* templates/deployment.yaml: add initContainer to fix EFS mount permission.
* values.yaml: add `persistence.useFsgroupInitContainer: BOOL` to control initContainer.

## Summary

NFS (EFS) could not control access control with normal Persistance Volume AccessControl.

> * [Configure a Pod to Use a PersistentVolume for Storage \- Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#access-control)

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv1
  annotations:
    pv.beta.kubernetes.io/gid: "1234"
```

Also StorageClass control not works neither.

Workaround is fix access control with initContainer.

## REF

> * [Persistent storage](https://cloud.ibm.com/docs/containers?topic=containers-cs_troubleshoot_storage#nonroot)
> * [fsGroup securityContext does not apply to nfs mount · Issue \#260 · kubernetes/examples](https://github.com/kubernetes/examples/issues/260)