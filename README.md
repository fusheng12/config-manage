# config-manage
# 1.介绍
一个ansible playbook 的角色，用来同步 ansible 主机目录上的配置文件，配置文件的目录可以按这种格式放置：config/appName/*
```
config/
├── common
│   ├── access.yaml
│   ├── values-prod-env.yaml
│   └── values-with-nodeport.yaml
├── iam-apiserver
│   └── iam-apiserver.yaml
├── iam-authz-server
│   └── iam-authz-server.yaml
├── iamctl
├── iam-pump
│   └── iam-pump.yaml
└── iam-watcher
    └── iam-watcher.yaml
```
# 2.使用
```
# iam-apiserver.yml
- hosts: iamctl
  vars:
    src_dir: /data/config
    app_name: iamctl
  roles:
    - role: config-manage
```

# 3.host文件
```
[iam-watcher]
192.168.40.61 ansible_ssh_user=root ansible_ssh_pass=redhat
192.168.40.62 ansible_ssh_user=root ansible_ssh_pass=redhat

[iamctl]
192.168.40.60 ansible_ssh_user=root ansible_ssh_pass=redhat
```

# 4.执行
```ansible-playbook -i hosts file.yaml ```

# 5.结果
```
[root@middleware-node01 app]# pwd
/home/service/app
[root@middleware-node01 app]# tree iamctl/
iamctl/
└── config
    ├── access.yaml
    ├── values-prod-env.yaml
    └── values-with-nodeport.yaml
```