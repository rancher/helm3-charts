vSphere Cloud Storage Interface (CSI)

1. This chart deploys manifests from the [kubernetes-sigs/vsphere-csi-driver](https://github.com/kubernetes-sigs/vsphere-csi-driver/tree/release-2.1/manifests/v2.1.0/vsphere-7.0u1/vanilla ) repository, following the steps mentioned in [this](https://vsphere-csi-driver.sigs.k8s.io/features/vsphere_csi_migration.html) tutorial.
2. As mentioned in the tutorial, the CSI requires the vsphere cloud-config to be provided via a Secret. This chart contains a manifest that can be used to create this Secret by providing the required values through values.yaml
3. It also provides the option of creating a StorageClass that uses the `csi.vsphere.vmware.com` as provsioner.
4. You can also modify the nodeSelectors for the CSI controller by providing the required selector in values.yaml