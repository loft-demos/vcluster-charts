# vCluster Chart for Embedded K8s Binaries
Customized vCluster Helm chart for use with custom vcluster container images that embed Kubernetes binaries directly into the vCluster container image instead of the Kubernetes binaries being copied from upstream container images attached as init containers to the vCluster `Pod`.

The `.tgz` for the chart may be downloades from the [repository releases](https://github.com/loft-demos/vcluster-charts/releases) and the chart is meant to be used with the vcluster-pro images published in the [loft-demos/k8s-image-mirror GHCR](https://github.com/loft-demos/k8s-image-mirror/pkgs/container/vcluster-pro).

### Usage
Create a `vcluster.yaml` with the following values (along with any other additional configuration needed based on the [vCluster configuration reference documentation](https://www.vcluster.com/docs/vcluster/configure/vcluster-yaml/):

> [!NOTE]
> Currently only the `k8s` or plain vanilla Kubernetes distubtion is supported.

```yaml
controlPlane:
  advanced:
    # DefaultImageRegistry will be used as a prefix for all internal images deployed by vCluster or Helm. This makes it easy to
    # upload all required vCluster images to a single private repository and set this value. Workload images are not affected by this.
    defaultImageRegistry: "ghcr.io/loft-demos/"
  statefulSet:
    # the tag should match one of the tags of the loft-demos/k8s-image-mirror/ [vcluster-pro images with embeeded k8s binaries](),
    # such as: `vcluster-pro:0.22.3-k8s.v1.32.0`
    tag: 0.22.3-k8s.v1.32.0
```
Deploy a vCluster with vCluster embedded binaries chart:
```bash
helm repo add vcluster https://loft-demos.github.io/helm-charts
helm install my-vcluster vcluster/vcluster --values vcluster.yaml
```

