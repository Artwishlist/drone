# Drone on Kubernetes with SSL
## Scripts to deploy drone (server-agent) to Google Cloud Kubernetes

### Usage
You should have first setup [kube-lego](https://github.com/jetstack/kube-lego/) like so: [kube-lego with nginx](https://github.com/jetstack/kube-lego/)

The files you'll want to change are:
- create-disk.sh (size > 20 GB and the zone your cluster lives in)
- namespace everywhere if not staging
- 01-configmap-template.yaml -> 01-configmap.yaml (drone.orgs, drone.admin, drone.host)
- 02-secret-template.yaml -> 02-secret.yaml (everything)
- 05-ingress-tls.yaml (host.server.com in hosts and host)

Then you can run:
```bash
kubectl apply -f 00-namespace.yaml
kubectl apply -f 01-configmap.yaml
kubectl apply -f 02-secret.yaml
kubectl apply -f 03-service-grpc.yaml
kubectl apply -f 03-service-ui.yaml
kubectl apply -f 04-deployment-server.yaml
kubectl apply -f 04-deployment-agent.yaml
kubectl apply -f 05-ingress-tls.yaml
```

### Future Changes
At some point we may provide a bash script to ask you and fill in all the required details.

Any contributions or issue reporting is welcome!

### Many thanks
- [drone](https://github.com/drone/drone)
- [kube-lego](https://github.com/jetstack/kube-lego/)
- [Let's Encrypt](https://letsencrypt.org/)
