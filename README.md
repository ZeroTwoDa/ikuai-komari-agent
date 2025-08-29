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
- 🚀 一键安装部署

## 🚀 快速开始

### 一键安装（推荐）

```bash
# 下载并运行一键安装脚本
curl -fsSL https://raw.githubusercontent.com/ZeroTwoDa/ikuai-komari-agent/main/install.sh | sudo bash
```
- **iKuai地址**: 如 `http://192.168.1.1`
- **iKuai用户名**: 如 `komari_user`
- **iKuai密码**: 输入密码（不会显示）
- **Komari服务器地址**: 如 `https://komari.server.com`
- **Komari认证令牌**: 输入认证令牌

#### 自动安装过程

脚本会自动执行以下步骤：

1. ✅ 检查系统类型和权限
2. ✅ 安装系统依赖（Python3、pip、venv等）
3. ✅ 创建Python虚拟环境
4. ✅ 复制程序文件到 `/opt/ikuai_Komari_agent`
5. ✅ 安装Python依赖包
6. ✅ 创建配置文件
7. ✅ 创建systemd服务
8. ✅ 启动服务并验证


### 手动安装

1. **下载ikuai_komari_agent.py ikuai_client.py config.py到服务器文件目录中**

2. **修改config.py文件中的配置项**

3. **安装系统依赖 创建虚拟环境并运行 使用systemd服务保活**

## 📋 系统要求

- **操作系统**: Debian 11+, Ubuntu 18.04+, CentOS 7+, RHEL 7+
- **Python**: Python 3.6+
- **权限**: root权限（用于安装系统服务和依赖）
- **网络**: 能够访问iKuai路由器和Komari服务器

## 📦 安装过程

### 自动安装流程

1. ✅ 检查系统类型和权限
2. ✅ 安装系统依赖（Python3、pip、venv等）
3. ✅ 从GitHub下载最新代码
4. ✅ 创建Python虚拟环境
5. ✅ 复制程序文件到 `/opt/ikuai_Komari_agent`
6. ✅ 安装Python依赖包
7. ✅ 交互式配置iKuai和Komari连接信息
8. ✅ 创建systemd服务
9. ✅ 启动服务并验证

### 配置信息

安装过程中需要输入以下信息：

- **iKuai地址**: 如 `http://192.168.1.1`
- **iKuai用户名**: 如 `komari_user`
- **iKuai密码**: 输入密码（不会显示）
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
├── install.sh               # 一键安装脚本
└── README.md                # 说明文档
```

## 🔄 卸载

### 使用脚本卸载

```bash
# 运行部署脚本选择卸载选项
sudo ./install.sh
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
