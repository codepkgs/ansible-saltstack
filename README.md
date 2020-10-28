# 使用前需知

1. 使用前需要确保每台主机都设置了主机名，`salt-minion` 的 `id` 基于主机名，为了确保 `salt-master` 能够正常的签发 `salt-minion` 的证书，建议每台机器主机名使用 `*.domain.local` 这种格式的 `FQDN`， 如 `master.fdisk.cc`。

2. `salt master` 中 `file_root` 和 `pillar_root` 默认值，一般不用修改。

```yaml
# file_roots 配置
file_roots:
  base:
    - /srv/salt/salt/base

# pillar_roots 配置
pillar_roots:
  base:
    - /srv/salt/pillar/base
```

3. 使用前需要修改 `hosts` 文件，文件格式如下：

```ini
# salt master 机器组。
[salt_master]
10.0.100.1      ansible_user=root

# salt minion 机器组。
[salt_minion]
10.0.100.1      ansible_user=root
10.0.100.2      ansible_user=root

# 用于 salt master 自动签发 minion 的证书
[salt_master:vars]
autosign_hosts = [ "*.fdisk.cc" ]

# salt minion 指定 salt master 的地址。如果指定的是域名，则确保该域名可以解析。
[salt_minion:vars]
salt_master = ["10.0.100.1"]
```

# 使用

```bash
# master 到所有的 minion 已经设置的免密码登录
ansible-playbook main.yaml

# master 到所有的 minion 没有设置免密码登录
ansible-playbook main.yaml -k
```
