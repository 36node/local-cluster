# mongodb

当前安装的 mongodb 版本为 4.4.4

## 参考命令行安装

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-release bitnami/mongodb
```

## 调试 mongodb

```
kubectl port-forward --namespace data svc/mongodb-headless 27017:27017
```

## 如果需要手动写入或者修改数据，需要连到 primary 数据库

```
kubectl -n data port-forward mongodb-0 37017:27017
```
