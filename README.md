# fahclient
Helm Chart for Folding at Home Client (FAHClient)

Install Folding@Home on Kubernetes

## TL;DR

Install `jq`.

Until [this](https://github.com/johnktims/folding-at-home/pull/10) PR is released to drop privileges inside the container use:

```bash
export FAHCLIENT_RELEASE_VERSION="$(curl -s https://api.github.com/repos/pcktdmp/fahclient/releases/latest | jq -r .tag_name)"
helm install https://github.com/pcktdmp/fahclient/archive/"${FAHCLIENT_RELEASE_VERSION}".tar.gz --set securityContext.runAsNonRoot=false --name fahclient
```

Once released use:

```bash
export FAHCLIENT_RELEASE_VERSION="$(curl -s https://api.github.com/repos/pcktdmp/fahclient/releases/latest | jq -r .tag_name)"
helm install https://github.com/pcktdmp/fahclient/archive/"${FAHCLIENT_RELEASE_VERSION}".tar.gz --name fahclient
```