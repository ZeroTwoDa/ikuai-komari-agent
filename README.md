# iKuai Komari 监控代理

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.6+-blue.svg)](https://www.python.org/)
[![Platform](https://img.shields.io/badge/platform-Linux-lightgrey.svg)](https://www.linux.org/)

一个用于监控iKuai路由器并将数据上报到Komari服务器的Python代理程序。

## ✨ 功能特性

- 🔄 实时监控iKuai路由器状态
- 📊 自动上报数据到Komari服务器
- 🔐 智能会话管理和自动重连
- 📝 优化的日志输出
- 🛡️ 完善的错误处理

## 🚀 快速开始

### Docker部署（推荐）

**环境要求**: Docker + Docker Compose

```bash
# 1. 克隆项目
git clone https://github.com/ZeroTwoDa/ikuai-komari-agent.git
cd ikuai-komari-agent

# 2. 配置参数（编辑config.py文件）
nano config.py

# 3. 启动服务
docker-compose up -d

# 4. 查看日志
docker-compose logs -f ikuai-komari-agent
```

详细Docker部署文档：[README_DOCKER.md](README_DOCKER.md)

### 传统部署方式

[安装文档](https://github.com/ZeroTwoDa/ikuai-komari-agent/blob/main/Install.md)

### 配置信息

安装过程中需要输入以下信息：

- **iKuai地址**: 如 `http://192.168.1.1`
- **iKuai用户名**: 如 `komari_user`
- **iKuai密码**: 如 `komari_password`
- **Komari服务器地址**: 如 `https://komari.server.com`
- **Komari认证令牌**: 输入认证令牌

## 🔧 服务管理

安装完成后，可以使用以下命令管理服务：

```bash
# 查看服务状态
sudo systemctl status ikuai_Komari_agent

# 启动服务
sudo systemctl start ikuai_Komari_agent

# 停止服务
sudo systemctl stop ikuai_Komari_agent

# 重启服务
sudo systemctl restart ikuai_Komari_agent

# 查看实时日志
sudo journalctl -u ikuai_Komari_agent -f

# 查看程序日志
sudo tail -f /opt/ikuai_Komari_agent/ikuai_agent.log
```

## 📊 监控数据

程序会监控并上报以下数据：

- **CPU使用率**：实时CPU使用情况
- **内存使用**：总内存和已使用内存
- **磁盘使用**：总容量和已使用空间
- **网络流量**：实时上传/下载速度和总流量
- **连接数**：当前TCP连接数
- **运行时间**：iKuai路由器运行时间
- **负载信息**：基于CPU使用率的智能估算

## 🔒 安全建议

### iKuai账户设置

为了安全和权限管理，建议在iKuai Web页面中创建一个单独的账户用于此代理程序：

1. **登录iKuai Web管理界面**
2. 导航到 **系统设置** → **登录管理** → **账号设置**
3. 点击 **添加** 或 **修改** 现有账户
4. **用户名**：例如 `komari_user`
5. **密码**：设置一个强密码
6. **允许访问IP**：设置为部署代理机器的内网IP地址
7. **默认权限**：选择 **新功能可见**
8. **登录状态超时时间**：设置为最高 `999` 分钟
9. **权限等级设置**：
   - 在 **页面权限** 列表中，只勾选 **访问** 列
   - 确保 **修改** 列全部不勾选，以限制代理程序只能读取数据



## 🗂️ 项目结构

```
ikuai-komari-agent/
├── ikuai_komari_agent.py    # 主程序
├── ikuai_client.py          # iKuai API客户端
├── config.py                # 配置文件模板
└── README.md                # 说明文档
```

### 手动卸载

```bash
# 停止服务
sudo systemctl stop ikuai_Komari_agent

# 禁用服务
sudo systemctl disable ikuai_Komari_agent

# 删除服务文件
sudo rm /etc/systemd/system/ikuai_Komari_agent.service

# 重新加载systemd
sudo systemctl daemon-reload

# 删除安装目录
sudo rm -rf /opt/ikuai_Komari_agent
```

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## ⭐ 星标

如果这个项目对您有帮助，请给它一个星标 ⭐

---

**注意**: 请确保在使用前正确配置iKuai路由器和Komari服务器的连接信息。 
