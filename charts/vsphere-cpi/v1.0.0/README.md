# vSphere Cloud Provider Interface (CPI)

[vSphere Cloud Provider Interface (CPI)](https://github.com/kubernetes/cloud-provider-vsphere) is responsible for running all the platform specific control loops that were previously run in core Kubernetes components like the KCM and the kubelet, but have been moved out-of-tree to allow cloud and infrastructure providers to implement integrations that can be developed, built and released independent of Kubernetes core. The official documentation and tutorials can be found [here](https://vsphere-csi-driver.sigs.k8s.io/driver-deployment/prerequisites.html).

## Prerequisites

- vSphere 6.7U3+
- Secret with vSphere credentials

## Installation

1. Before installing the chart, you need to create a secret in the chart's namespace with the server URL and credentials to connect to the vCenter. To create a secret in Rancher, go to your cluster's project (Same project you will be installing the chart) > Resources > Secrets > Add Secret
    ```yaml
    # Example of data required in the secret
    <host-1>.username: <username>
    <host-1>.password: <password>
    ```

2. Install the chart, and make sure to provide the same name of the credential's secret you created.

## Migration

If using this chart to migrate volumes provisioned by the in-tree provider to the out-of-tree CPI + CSI, you need to taint all nodes with the following:
```
node.cloudprovider.kubernetes.io/uninitialized=true:NoSchedule
```

A script [taints.sh](../taints.sh) has been added for your convenience, and it can be executed with the following command:
```
# Optionally, a path to a kube config can be provided for cases
# where the script needs to be executed from outside of the cluster
./taints.sh <optional-path-to-kubeconfig>
```
