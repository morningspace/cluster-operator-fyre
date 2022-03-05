# Cluster Operator Fyre

An Ansible Operator used to provision OpenShift cluster on Fyre by calling Fyre REST APIs.

## Installation

To install this operator, run:

```shell
make deploy
```

This will install the operator onto your target Kubernetes cluster that is currently being used. (The current context specified in your kubeconfig)

## How to use

For example, if you want to provision an OCP cluster with version `4.8.27` and `medium` size on Fyre QuickBurn, you can apply below Kubernetes resource:

```yaml
apiVersion: clusters.ibm.com/v1alpha1
kind: OpenShiftFyre
metadata:
  name: openshiftfyre-qb-medium
  namespace: cluster-operator-fyre-system
spec:
  # Reference to a secret including your fyre credential
  providerSecretRef: my-fyre-secret
  # Using Quick Burn
  quotaType: "quick_burn"
  # Site location
  site: "svl"
  # OCP version
  ocpVersion: "4.8.27"
  # Platform using x86
  platform: "x"
  # Size using medium
  size: "medium"
```

Before that, you may also need to create a secret including your Fyre credential that will be used by the operaor to communicate with Fyre REST APIs.

```sh
kubectl create secret generic my-fyre-secret -n cluster-operator-fyre-system \
  --from-literal username=<your fyre user name> \
  --from-literal password=<your fyre user token> \
  --from-literal product_group_id=<your fyre group id> \
```

You can find more examples in `config/samples` directory.
