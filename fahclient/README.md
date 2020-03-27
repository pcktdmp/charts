# fahclient
Helm Chart for Folding at Home Client (FAHClient)

Install [Folding@Home](https://foldingathome.org/) on Kubernetes

## Motivation

Learned about the Folding@Home initiative during the COVID-19 crisis.

https://foldingathome.org/2020/03/15/coronavirus-what-were-doing-and-how-you-can-help-in-simple-terms/

Companies, enterprises and individuals can donate their compute capacity that is available inside their Kubernetes clusters to foldingathome.org.

## Features

* Make use of `StatefulSet` with Persistent Volumes so that compute capacity does not get lost when being rescheduled on other nodes.
This fits for example the design pattern of using Spot Instances in AWS EKS.
* Horizontal Pod Autoscaling
q
## TL;DR

```bash
helm repo add pcktdmp https://pcktdmp.github.io/charts
helm install pcktdmp/fahclient --name fahclient
```

## Support

If you need basic support to getting up and running please
drop me an e-mail at <serge@se-cured.org>.

## FAQ

Q: I want to stop folding but don't want work to be lost, what do I need to do?
A: Assuming you have the pods running in a separate namespace where no other pods reside: `kubectl get pods -n <yournamespace> | awk '{print $1}' | xargs -I{} kubectl exec {} -- /usr/bin/FAHClient --send-finish`.