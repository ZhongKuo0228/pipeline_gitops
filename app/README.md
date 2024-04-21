# K8s 測試

## 自簽證書方式

參考這篇教學：https://blog.niclin.tw/2019/08/16/creating-self-signed-certificate-using-openssl/

## K8s Secret Type

[K8s 官方說明 `Secret type` ](https://kubernetes.io/docs/concepts/configuration/secret/#tls-secrets)可以使用 `kubernetes.io/tls` 和 `Opaque`，兩者並無差異，只是 `kubernetes.io/tls` 比較方便管理，基本上專案內是使用的 type 一致就好

## K8s Apply

1. 先 apply `nginx-conf.yaml` 和 `ssl-secrets.yaml`
2. 再 apply `pod.yaml`
3. `service.yaml` 不一定要用，也可以進入到 Pod 內做測試
4. 如果使用有建立 service，可以使用除錯的 `curl` pod 來測試
```
kubectl run --restart=Never --rm -it curl --image curlimages/curl -- sh
```
去 curl `service` 的 ClusterIP 即可

## 測試 Custom Domain Header


```
curl -k -H "X-Custom-Domain: your-custom-domain.com" https://localhost/
```
