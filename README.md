## installation
```
# create namespace
$ kubectl create ns monitoring

# create pv/pvc
$ kubectl apply -f prometheus/pv.yaml
$ kubectl apply -f prometheus/pvc.yaml
```
### prometheus
```
$ helm install prometheus stable/prometheus -f prometheus/values.yaml --namespace monitoring
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
```
