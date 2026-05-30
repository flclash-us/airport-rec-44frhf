# Trojan-Go 配置完全指南

Trojan-Go 是 Trojan 的 Go 语言实现，支持 WebSocket 和多路复用。

## Trojan vs Trojan-Go

| 特性 | Trojan | Trojan-Go |
|------|--------|-----------|
| WebSocket | No | Yes |
| 多路复用 | No | Yes |
| 路由器负载 | 高 | 低 |

## 安装

```bash
# 一键安装
bash <(curl -s https://raw.githubusercontent.com/p4gefau1t/trojan-go/install.sh)

# 或 Docker
docker run -d --name trojan-go \
  -v /opt/trojan-go/config.json:/etc/trojan-go/config.json \
  -p 443:443 --restart always trojan-go
```

## 配置文件

```json
{
  "run_type": "server",
  "local_addr": "0.0.0.0",
  "local_port": 443,
  "remote_addr": "www.example.com",
  "remote_port": 443,
  "password": ["your-password"],
  "ssl": {
    "cert": "/path/to/cert.pem",
    "key": "/path/to/key.pem"
  },
  "websocket": {
    "enabled": true,
    "path": "/trojan-go",
    "host": "www.example.com"
  }
}
```

## 核心原理

Trojan 伪装成正常 HTTPS 流量：

```
正常用户 > 访问伪装网站 > 显示正常内容
Trojan用户 > TLS握手 > 解密 > 代理流量
           ^
        443端口无法区分
```

## 常见问题

**和 V2Ray VLESS 哪个好？** VLESS Reality 更抗封锁；Trojan-Go 更简单易用。

---

推荐工具：

- [Clash for Windows](https://clashforwindows.site/)
- [ClashMI](https://clashmi.site/)
- [FlClash](https://flclash.us/)
