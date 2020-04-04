## installation
```
# create namespace
$ kubectl create ns monitoring

# create pv/pvc
## set up NFS before deploying
$ kubectl apply -f grafana/nfs-pv.yaml
$ kubectl apply -f grafana/nfs-pvc.yaml
$ kubectl apply -f prometheus/nfs-pv.yaml
$ kubectl apply -f prometheus/nfs-pvc.yaml
```
### prometheus
```
$ helm install prometheus stable/prometheus --version v10.6.0 -f prometheus/values.yaml --namespace monitoring

# use extraScrapeConfigs
$ helm install prometheus stable/prometheus --version v10.6.0 -f prometheus/values.yaml --set-file extraScrapeConfigs=prometheus/extraScrapeConfigs.yaml --namespace monitoring
```

### grafana
```
$ helm install grafana stable/grafana -f grafana/values.yaml --namespace monitoring
```

## GUI
```
# prometheus
$ open http://$(kubectl get nodes --namespace monitoring -o jsonpath="{.items[0].status.addresses[0].address}"):$(kubectl get --namespace monitoring -o jsonpath="{.spec.ports[0].nodePort}" services prometheus-server)

# grafana
$ open http://$(kubectl get nodes --namespace monitoring -o jsonpath="{.items[0].status.addresses[0].address}"):$(kubectl get --namespace monitoring -o jsonpath="{.spec.ports[0].nodePort}" services grafana)

## get password
$ kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 -D
```
