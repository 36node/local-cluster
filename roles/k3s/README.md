# k3s

ansible 安装 k3s 集群, 利用 k3sup 进行简便安装

## 准备控制机

- 安装 ansible
- 安装 python
- 安装 kubectl

pip install openshift===0.11.0
pip install kubernetes===11.0.0
pip install pyyaml

## Ingress

使用 k3s 自带的 traefic, 需要加上 `kubernetes.io/ingress.class: traefik`

书写样例

```yaml
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: bus-admin-pudong-airport
  annotations:
    kubernetes.io/ingress.class: traefik
    cert-manager.io/cluster-issuer: letsencrypt-alidns
    # traefik.ingress.kubernetes.io/redirect-entry-point: https
spec:
  rules:
    - host: pudongair.36node.com
      http:
        paths:
          - backend:
              serviceName: bus-admin-pudong-airport
              servicePort: 80
            path: /
  tls:
    - secretName: pudongair.36node.com
      hosts:
        - pudongair.36node.com
```

## Excluding the Service LB from Nodes

To exclude nodes from using the Service LB, add the following label to the nodes that should not be excluded:

```
svccontroller.k3s.cattle.io/enablelb
```

If the label is used, the service load balancer only runs on the labeled nodes.

k3s 启动的时候，可以用 --label-nodes 去关闭或者开启节点的 lb 功能

## private registry

https://rancher.com/docs/k3s/latest/en/installation/private-registry/

## k8s 相关命令

查看日志

- systemctl status kubelet 确认状态
- journalctl -u kubelet 查看错误日志
- journalctl -u k3s 查看 k3s 的日志
- journalctl -xe

查看 k8s 资源版本

```
kubectl explain cronjob
```

## 错误解决

1. invalid capacity 0 on image filesystem

https://github.com/ubuntu/microk8s/issues/401#issuecomment-480945986

## 重新创建 kubeconfig

```
k3sup install --skip-install \
    --ip "{{ k8s_lb }}" \
    --user "{{ ansible_user }}" \
    --context {{ k8s_cluster_name }} \
    --local-path ~/.kube/config.{{ k8s_cluster_name }} \
    --k3s-extra-args '--tls-san {{ k8s_lb }} --node-label svccontroller.k3s.cattle.io/enablelb=true' \
    --ssh-key {{ ansible_private_key_file }} \
    --cluster
```
