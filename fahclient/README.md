# fahclient
Helm Chart for Folding@Home Client (FAHClient)

Install [Folding@Home](https://foldingathome.org/) on Kubernetes

## Motivation

Learned about the Folding@Home initiative during the COVID-19 crisis.

https://foldingathome.org/2020/03/15/coronavirus-what-were-doing-and-how-you-can-help-in-simple-terms/

Companies, enterprises and individuals can donate their compute capacity that is available inside their Kubernetes clusters to foldingathome.org.

## Features

* Make use of `StatefulSet` with Persistent Volumes so that compute capacity does not get lost when being rescheduled on other nodes.
This fits for example the design pattern of using Spot Instances in AWS EKS.
* [Horizontal Pod Autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
* [Vertical Pod Autoscaling](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler)

## TL;DR

```bash
helm repo add pcktdmp https://pcktdmp.github.io/charts
helm install pcktdmp/fahclient --name fahclient
```
## Support

If you need basic support to getting up and running please
drop me an e-mail at <serge@se-cured.org>.

## Chart Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| fahClient.extraArgs | object | `{}` | Extra arguments for `FAHClient`, passed like `- --somearg=value`  |
| fahClient.power | string | `"full"` |  Valid values are `light`, `medium`, `full` |
| fahClient.smp | bool | `true` |  |
| fahClient.team | int | `0` | Team identifier |
| fahClient.user | string | `"Anonymous"` | The user you identify yourself with to Folding@Home |
| fullnameOverride | string | `""` |  |
| horizontalPodAutoscaling.enabled | bool | `false` |  |
| horizontalPodAutoscaling.maxReplicas | int | `1` |  |
| horizontalPodAutoscaling.minReplicas | int | `1` |  |
| horizontalPodAutoscaling.targetCPUUtilizationPercentage | int | `90` |  |
| storageClassName | string | `""` | When not specified take the default storage class |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"johnktims/folding-at-home"` |  |
| image.tag | string | `"latest"` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| nameOverride | string | `""` |  |
| podSecurityContext.fsGroup | int | `9999` |  |
| priorityClassName | string | `nil` | When not specified, take the default priority class |
| replicaCount | int | `1` |  |
| resources.limits.cpu | float | `1` |  |
| resources.limits.memory | string | `"256Mi"` |  |
| resources.requests.cpu | float | `1` |  |
| resources.requests.memory | string | `"128Mi"` |  |
| securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| securityContext.readOnlyRootFilesystem | bool | `false` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `9999` |  |
| service.port | int | `80` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `nil` |  |
| verticalPodAutoscaling.enabled | bool | `false` |  |
| verticalPodAutoscaling.updateMode | string | `"Auto"` | Valid values are `Auto`, `Recreate`, `Initial`, `Off`  |

## FAQ

Q: I want to stop folding but don't want work to be lost, what do I need to do?

A: Assuming you have the pods running in a separate namespace where no other pods reside:
`kubectl get pods -n <yournamespace> | awk '{print $1}' | xargs -I{} kubectl exec {} -- /usr/bin/FAHClient --send-finish`.

Q: How do I set up persistent storage for my cluster quickly?

A: Setup an NFS server in your network or leverage an existing one and setup [nfs-client-provisioner](https://github.com/kubernetes-incubator/external-storage/tree/master/nfs-client).
