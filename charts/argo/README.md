## Argo Workflows Chart

This is a **community maintained** chart. It is used to set up argo and it's needed dependencies through one command. This is used in conjunction with [helm](https://github.com/kubernetes/helm).

If you want your deployment of this helm chart to most closely match the [argo CLI](https://github.com/argoproj/argo), you should deploy it in the `kube-system` namespace.

## Usage Notes:
This chart defaults to setting the `controller.instanceID.enabled` to `false` now, which means the deployed controller will act upon any workflow deployed to the cluster.  If you would like to limit the behavior and deploy multiple workflow controllers, please use the `controller.instanceID.enabled` attribute along with one of it's configuration options to set the `instanceID` of the workflow controller to be properly scoped for your needs.

## Values

The `values.yaml` contains items used to tweak a deployment of this chart.
Fields to note:
* `controller.instanceID.enabled`: If set to true, the Argo Controller will **ONLY** monitor Workflow submissions with a `--instanceid`  attribute
* `controller.instanceID.useReleaseName`: If set to true then chart set controller instance id to release name
* `controller.instanceID.explicitID`: Allows customization of an instance id for the workflow controller to monitor
* `controller.workflowNamespaces`: This is a list of namespaces where workflows will be ran
* `minio.install`: If this is true, we'll install [minio](https://github.com/kubernetes/charts/tree/master/stable/minio) and build out the artifactRepository section in workflow controller config map.
* `artifactRepository.s3.accessKeySecret` and `artifactRepository.s3.secretKeySecret` These by default link to minio default credentials stored in the secret deployed by the minio chart.
