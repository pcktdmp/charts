# fahclient
Helm Chart for Folding at Home Client (FAHClient)

Install [Folding@Home](https://foldingathome.org/) on Kubernetes

## Motivation

Learned about the Folding@Home initiative in the COVID-19 crisis.

https://foldingathome.org/2020/03/15/coronavirus-what-were-doing-and-how-you-can-help-in-simple-terms/

Companies, enterprises and individuals can donate their compute capacity that is available inside their Kubernetes clusters to foldingathome.org.

## TL;DR

Until [this](https://github.com/johnktims/folding-at-home/pull/10) PR is released to drop privileges inside the container use:

```bash
helm repo add pcktdmp https://pcktdmp.github.io/charts
helm install pcktdmp/fahclient --set securityContext.runAsNonRoot=false --name fahclient
```

Once released use:

```bash
helm repo add pcktdmp https://pcktdmp.github.io/charts
helm install pcktdmp/fahclient --name fahclient
```