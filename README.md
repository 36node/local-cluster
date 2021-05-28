# local-cluster

本地集群的部署和运维

## Prepares

- [helm3](https://github.com/helm/helm#install)
- [安装 k3sup 脚本](https://github.com/alexellis/k3sup#download-k3sup-tldr)，`brew install k3sup`
- 安装 ansible, `brew install ansible`
- 安装 python3, pip3, mac 已经预装，可以考虑更新
- 安装下方的 pip 依赖
- gem install dotenv

安装一些 python 依赖， TODO: 这部分已有也写到脚本里，通过 yarn 执行

```
pip install ansible // mac 已通过 brew 安装
pip install kubernetes===11.0.0
pip install openshift===0.12.0
```

## Quick Start

准备环境变量

```
cp env.example .env

// 编辑 .env 文件
```

一键部署，由集群管理员操作

```
yarn
yarn site
```

将包含:

- 集群环境
- TODO: 集群监控
- avatar
  - kafka
  - elasticsearch
  - vector

一键清空所有部署:

```
yarn clean
```

### 重置 ssh key，有超级管理员执行

```
// 1. 准备新的 pub_keys/id_rsa_c_ctyun.pub
// 2. 重新授权，如果加 reset 将排除所有其他 key
yarn auth -e "reset=yes"
```

### k8s

可视化管理采用 lens

```
brew install lens
```

## 跳板机美化

跳板机默认安装有 zsh，可以使用 [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh#getting-started) 进行个性化配置
