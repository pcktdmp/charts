# fahclient
Helm Chart for Folding at Home Client (FAHClient)

Install Folding@Home on Kubernetes

Until (this)[https://github.com/johnktims/folding-at-home/pull/10 PR has not been released inside the image use:

```bash
helm install https://github.com/pcktdmp/fahclient/archive/0.1.1.tar.gz --set securityContext.runAsNonRoot=false --name fahclient
```

Once released use:

```bash
helm install https://github.com/pcktdmp/fahclient/archive/0.1.1.tar.gz --name fahclient
```