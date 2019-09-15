---
title: ssr常用命令 与锐速常用命令
date: 2019-08-07 10:40:38
tags: ssr
---

## ssr

- 启动
  
  /etc/init.d/shadowsocks start

- 停止
  
  /etc/init.d/shadowsocks stop

- 重启
  
  /etc/init.d/shadowsocks restart

- 状态
  
  /etc/init.d/shadowsocks status

- 修改密码
  
  1.输入vi/etc/shadowsocks.json

  2.按“i”进入编辑模式，编辑如下：

  ```json
    { 
      "server": "0.0.0.0",
      "server_ipv6": "::",      
      "local_address": "127.0.0.1", 
      "local_port": 1081, 
      "port_password":
      { 
        "端口1":"密码1", 
        "端口2":"密码2", 
        "端口3":"密码3", 
        "端口4":"密码4" 
      }, 
      "timeout": 120, 
      "udp_timeout": 60, 
      "method": "chacha20", 
      "protocol": "auth_sha1_compatible", 
      "protocol_param": "", 
      "obfs": "http_simple_compatible", 
      "obfs_param": "", 
      "dns_ipv6": false, 
      "connect_verbose_info": 0, 
      "redirect": "", 
      "fast_open": false, 
      "workers": 1 
    }
  ```

  3.按“i”进入编辑模式，编辑如下：
  
  按esc返回，输入:wq回车保存

  4.输入/etc/init.d/shadowsocks restart重启ssr

  5.如不能联网，则关闭防火墙（逐条输入）
  ```bash
  service iptables restart
  service iptables stop chkconfig iptables off
  ```

## 锐速
- 重启锐速：

/serverspeeder/bin/serverSpeeder.sh restart

- 锐速状态：

/serverspeeder/bin/serverSpeeder.sh status

- 卸载锐速：

chattr -i /serverspeeder/etc/apx* && /serverspeeder/bin/serverSpeeder.sh uninstall -f