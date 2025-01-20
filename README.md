# vCluster Chart for Embedded K8s Binaries
Customized vCluster Helm chart for use with custom vcluster container images that embed Kubernetes binaries directly into the vCluster container image instead of the Kubernetes binaries being copied from upstream container images attached as init containers to the vCluster `Pod`.

The `.tgz` for the chart may be downloades from the [repository releases](https://github.com/loft-demos/vcluster-charts/releases) and the chart is meant to be used with the vcluster-pro images published in the [loft-demos/k8s-image-mirror GitHub Container Registry](https://github.com/loft-demos/k8s-image-mirror/pkgs/container/vcluster-pro).

## Usage
Create a `vcluster.yaml` with the following values (along with any other additional configuration needed based on the [vCluster configuration reference documentation](https://www.vcluster.com/docs/vcluster/configure/vcluster-yaml/):

> [!NOTE]
> Currently, only the [vanilla Kubernetes distribution](https://kubernetes.io/releases/) is supported. `k8s` is the default `controlPlane.distro` and is enabled by default, so no additional configuration is needed for the `distro`.

```yaml
controlPlane: 
  statefulSet:
    image:
      registry: "ghcr.io/loft-demos/"
      repository: vluster-pro
      # the tag should match one of the tags of the loft-demos/k8s-image-mirror/ [vcluster-pro images with embeeded k8s binaries](https://github.com/loft-demos/k8s-image-mirror/pkgs/container/vcluster-pro),
      # such as: `vcluster-pro:0.22.3-k8s.v1.32.0`
      tag: 0.22.3-k8s.v1.32.0
```

Deploy a vCluster with vCluster embedded binaries chart:
```bash
helm repo add vcluster https://loft-demos.github.io/helm-charts
helm install my-vcluster vcluster/vcluster --values vcluster.yaml
```

For Air-Gapped Environments:
```bash
helm install my-vcluster ./vcluster-0.22.3.tgz --values vcluster.yaml
```
