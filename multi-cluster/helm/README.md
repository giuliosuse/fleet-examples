# Multi-Cluster Helm Example

This example will deploy the [Kubernetes sample guestbook](https://github.com/kubernetes/examples/tree/master/guestbook/) application as
packaged as a Helm chart.
The app will be deployed into the `fleet-mc-helm-example` namespace.

The application will be customized as follows per environment:

* Dev clusters: Only the redis leader is deployed and not the followers.
* Test clusters: Scale the front deployment to 3
* Prod clusters: Scale the front deployment to 3 and set the service type to LoadBalancer

```yaml
kind: GitRepo
apiVersion: fleet.cattle.io/v1alpha1
metadata:
  name: helm
  namespace: fleet-default
spec:
  repo: https://github.com/giuliosuse/fleet-examples
  paths:
  - multi-cluster/helm
  targets:
  - name: dev
    clusterSelector:
      matchLabels:
        env: dev

  - name: test
    clusterSelector:
      matchLabels:
        env: test

  - name: prod
    clusterSelector:
      matchLabels:
        env: prod
```
