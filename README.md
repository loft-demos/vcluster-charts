# vcluster-charts
Customized vCluster Helm chart for use with custom vcluster container images that embed Kubernetes binaries directly into the vCluster container image instead of the Kubernetes binaries being copied from upstream container images attached as init containers to the vCluster `Pod`.

The `.tgz` for the chart may be downloades from the [repository releases](https://github.com/loft-demos/vcluster-charts/releases) and the chart is meant to be used with the vcluster-pro images published in the [loft-demos/k8s-image-mirror GHCR](https://github.com/loft-demos/k8s-image-mirror/pkgs/container/vcluster-pro).




