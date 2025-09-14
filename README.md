Thanks of https://github.com/aoi1/bbf-kubernetes

# kind

## create cluster
```
kind create cluster --image=kindest/node:v1.29.0
```

## delete cluster
```
kind delete cluster
```

# kubectl

## describe api resources
```
kubectl api-resources
```

## get nodes
```
kubectl get nodes
```

## get pod
```
kubectl get pod --namespace default
```

## apply manifest
```
kubectl apply --filename chapter-04/myapp.yaml --namespace default
```

## describe pod
```
kubectl describe pod myapp -n default
```

## get logs
```
kubectl logs myapp -n default
kubectl logs myapp -c hello-server -n default
```

※pod指定する場合は`--selector {k}={v}`でlabelで絞り込める

## debug
```
kubectl debug -it myapp --image=curlimages/curl:8.4.0 --target=hello-server -n default -- sh
```

※対象のコンテナと同じホスト・ボリュームを参照できる

## exec
```
kubectl -n default exec -it curlpod -- /bin/sh
```

## port forward
```
kubectl port-forward myapp 5555:8080 -n default
```

## edit manifest
```
kubectl edit pod myapp -n default
```

## show manifest diff
```
kubectl diff -f chapter-06/service-nodeport.yaml
```

## delete pod
```
kubectl delete pod myapp -n default
```

## get replicaset
```
kubectl get rs -n default
```

## delete replicaset
```
kubectl delete rs httpserver -n default
```

## get deployment
```
kubectl get deploy -n default
```

## get service
```
kubectl get service hello-server-service -n default
```

## cheat sheet
https://kubernetes.io/docs/reference/kubectl/quick-reference/
