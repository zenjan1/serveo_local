# serveo_local - Self-hosted Serveo Server

Serveo.net 是一种通过SSH进行端口转发的服务。本项目提供了搭建自托管Serveo服务器的完整指南和工具，不依赖于外部服务。

## 功能特点

- **HTTP端口转发**: 将本地HTTP服务暴露到公网
- **TCP端口转发**: 支持任意TCP服务的端口转发
- **Shell Wrapper**: 简化的命令行工具，一键创建隧道
- **多平台支持**: 支持Linux服务器部署

## 快速开始

### 服务器端部署

在服务器上（如DigitalOcean Ubuntu VPS）:

```bash
# 1. SSH登录服务器
# 2. 更新系统并安装依赖
sudo apt update && sudo apt upgrade -y

# 3. 下载serveo二进制文件（需要自行获取或编译）
# 注意：原始的Google Cloud Storage下载链接已不可用
# 请参考编译指南自行编译

# 4. 生成SSH主机密钥
ssh-keygen -t rsa -f ssh_host_rsa_key

# 5. 使用域名运行serveo
./serveo --port=2222 -domain=yourdomain.com

# 或后台运行
nohup ./serveo --port=2222 -domain=yourdomain.com &
```

### 客户端使用

```bash
# 连接到自托管的serveo服务器，将本地8000端口映射到公网80端口
ssh <server-ip> -p 2222 -R 80:localhost:8000 yourdomain.com
```

## Shell Wrapper (serveo)

项目中的 `serveo` 脚本是一个简化使用的shell包装器：

```bash
# HTTP隧道 - 使用自定义子域名
./serveo http <subdomain>

# TCP隧道 - 指定端口
./serveo tcp <port>

# 终止所有隧道进程
./serveo kill
```

## 编译指南

如果需要自行编译Serveo，请参考以下步骤：

1. 获取Serveo源码
2. 安装Go语言环境
3. 编译项目

## HTTPS支持（实验性）

请参考 `https-instructions-not-working.md` 文件了解HTTPS配置尝试（目前不工作）。

## 依赖要求

- SSH客户端（OpenSSH）
- 服务器端：具有SSH访问权限的服务器和域名

## 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 贡献

欢迎提交Issue和Pull Request！

## 注意事项

- 原始的serveo二进制文件下载链接已不可用，请自行编译或寻找替代方案
- 使用前请确保了解端口转发的安全风险
- 建议在生产环境中使用防火墙和安全组限制访问