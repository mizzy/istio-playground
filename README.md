# Istio Playground

## References

- [サービスメッシュを実現するIstioをEKS上で動かす – その1 まずはMinikubeでサンプルアプリケーションを動かしてみる – PSYENCE:MEDIA](https://tech.recruit-mp.co.jp/infrastructure/post-19169/)


## Run on minikube

### Install istio

```
$ minikube start --memory=8192 --cpus=4 --kubernetes-version=v1.13.0
$ curl -L https://git.io/getLatestIstio | ISTIO_VERSION=1.1.1 sh -
$ cd istio-1.1.1
$ for i in install/kubernetes/helm/istio-init/files/crd*yaml; do kubectl apply -f $i; done
$ kubectl apply -f install/kubernetes/istio-demo.yaml
$ kubectl get service --namespace istio-system
$ kubectl get pods --namespace istio-system
```

### Install sample application

```
$ kubectl label namespace default istio-injection=enabled
$ kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
$ kubectl get services
$ kubectl get pods
$ kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml
$ kubectl get pods --selector istio=ingressgateway --all-namespaces
$ minikube ip
$ kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}'
```
