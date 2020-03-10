## create namespace
```
$ kubectl create ns remo
```

## create secret
### create secret dir
```
$ mkdir secret
```

### create secret file
```
$ cat secret/api-keys
<Nature Remo access token>
```

## deploy resources
```
$ kubectl apply -k .
```
