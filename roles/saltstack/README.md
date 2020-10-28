# 作用
用于安装salt-master和salt-minion。

# 变量
```text
salt_role: master # 指定salt角色，master或minion
salt_master: saltmaster.fdisk.cc # salt master 服务器的地址，minion 端使用
master_publish_port: 4505 # master publish port，默认是4505
master_ret_port: 4506 # minion return port，默认是4506

# file_roots 配置
file_roots:
  base:
    - /srv/salt/base   # 这里指定的目录会自动创建

# pillar_roots 配置
pillar_roots:
  base:
    - /srv/salt/pillar

# 定义自动签发的主机列表。如果不需要自动签发，则不用定义该变量。定义在master角色的节点。
autosign_hosts
  - "*.fdisk.cc"
# minion_id: <minion_id> # 使用每个机器的FQDN作为minion_id，不要设置该变量。

# 是否仅显示差异（发生变化的ID）
state_output_diff: False
```