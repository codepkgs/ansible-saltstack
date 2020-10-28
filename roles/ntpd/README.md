# 说明

* 功能  

    该role用于安装并配置`ntp`服务，并关闭`chronyd`服务，如果没有配置ntp_servers变量，则采用阿里云的ntp服务器(`ntp.aliyun.com`).

* 变量
    ```text
    local_clock: 是否启用本地时间服务器。默认False，即不启用。
    ntp_servers: 定义ntp服务器的地址。列表。默认为 ntp.aliyun.com
    ntp_restrict: 定义允许哪些客户端进行时间同步。列表。需要有network和netmask字段。默认为空。
    ```

* 使用角色
    ```text
    - hosts: all
      roles:
        - role: ntp
          tags: ntp
          vars:
            ntp_servers:
              - ntp.aliyun.com
            ntp_restricts:
              - network: 10.0.100.0
                netmask: 255.255.0.0
    ```
