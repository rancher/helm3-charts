vSphere Cloud Provider Interface (CPI)

1. This chart deploys manifests from the [kubernetes/cloud-provider-vsphere](https://github.com/kubernetes/cloud-provider-vsphere) repository, following the steps mentioned in [this](https://vsphere-csi-driver.sigs.k8s.io/driver-deployment/prerequisites.html#vsphere_cpi) tutorial.
2. As mentioned in the tutorial, the CPI requires the vsphere cloud-config to be provided via a ConfigMap. It also requires the vSphere credentials to be provided via a Secret, which is then referred by the ConfigMap.
This chart provides manifests to create the Secret and the ConfigMap.
3. When this chart is used for migrating volumes provisioned using the in-tree provider to the out-of-tree CPI+CSI, all nodes need to be tainted with the following taint:
```
node.cloudprovider.kubernetes.io/uninitialized=true:NoSchedule
```
The script [taints.sh](../taints.sh) can be run for tainting the nodes using the following command:
```
taints.sh <path_to_kubeconfig (optional, if running outside the cluster)>
```
4. You can also modify the nodeSelectors for the CPI cloud-controller-manager by providing the required selector in values.yaml