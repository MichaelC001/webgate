# Webgate

个人 webhook 网关服务 - 外网到本地的桥梁。

## 架构

```
互联网 → Caddy (192.168.151.88:8443) → Webgate (localhost:8000) → 本地服务
```

## 端口映射

| 服务 | 外网端口 | 内网 | 说明 |
|------|----------|------|------|
| WireGuard | 51820 | 192.168.151.13 (NAS) | VPN |
| Caddy | 8443 | 192.168.151.88 (Mac) | 反向代理 |
| Webgate | - | localhost:8000 | 本服务 |

## 功能规划

- [ ] Notion webhook → note sync
- [ ] GitHub webhook → 通知推送
- [ ] 远程笔记 API
- [ ] 更多...

## 运行

```bash
cd ~/Documents/webgate
uvicorn main:app --host 0.0.0.0 --port 8000
```

## Caddy 配置

```caddyfile
webhook.niuniu.me {
    reverse_proxy localhost:8000
}
```

## 依赖

```bash
pip install fastapi uvicorn
```
