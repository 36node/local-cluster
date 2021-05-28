## 调试

kubectl run -i --tty --rm debug --image=busybox --restart=Never -- sh

## 追加 basic-auth 的用户

htpasswd -b roles/bus/files/auth username password
re-run playbook site.yml

## aliyun-cs.yml

作用是加入 k8s account，使得 cluster 可以获取阿里云镜像，目前利用 k3s 的配置，直接配置到整个集群

## 手动更新

kubectl patch deployment -n pudongbus bus-admin -p '{"spec":{"template":{"spec":{"containers":[{"name":"bus-admin","env":[{"name":"LAST_MANUAL_RESTART","value":"'$(date +%s)'"}]}]}}}}'
