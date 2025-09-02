# iKuai Komari 监控代理 - Docker部署版

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/docker-supported-blue.svg)](https://www.docker.com/)

一个用于监控iKuai路由器并将数据上报到Komari服务器的Python代理程序，现已支持Docker容器化部署。

## ✨ 功能特性

- 🔄 实时监控iKuai路由器状态
- 📊 自动上报数据到Komari服务器
- 🔐 智能会话管理和自动重连
- 📝 优化的日志输出
- 🛡️ 完善的错误处理
- 🐳 Docker容器化部署支持

## 🚀 Docker部署（推荐）

### 环境要求

- Docker
- Docker Compose

### 快速开始

1. **克隆项目**
```bash
git clone https://github.com/ZeroTwoDa/ikuai-komari-agent.git
cd ikuai-komari-agent
```

2. **配置参数**
```bash
# 复制配置文件模板
cp config.py config_local.py

# 编辑配置文件
nano config.py
```

在 `config.py` 中配置以下信息：
```python
# iKuai路由器配置
IKUAI_URL = "http://192.168.1.1"  # 你的iKuai路由器地址
IKUAI_USERNAME = "komari_user"    # iKuai用户名
IKUAI_PASSWORD = "komari_password" # iKuai密码

# Komari服务器配置
KOMARI_SERVER_URL = "https://komari.server.com"  # Komari服务器地址
KOMARI_TOKEN = "your_komari_token"               # Komari认证令牌

# 监控间隔（秒）
MONITOR_INTERVAL = 60
```

3. **启动服务**
```bash
# 使用Docker Compose启动
docker-compose up -d
```

4. **查看服务状态**
```bash
# 查看容器状态
docker-compose ps

# 查看实时日志
docker-compose logs -f ikuai-komari-agent

# 查看日志文件
tail -f logs/ikuai_agent.log
```

### 手动Docker部署

如果你想手动构建和运行Docker容器：

```bash
# 构建镜像
docker build -t ikuai-komari-agent .

# 运行容器
docker run -d \
  --name ikuai-komari-agent \
  -v $(pwd)/logs:/app/logs \
  -v $(pwd)/config.py:/app/config.py \
  --restart unless-stopped \
  ikuai-komari-agent
```

### 服务管理

```bash
# 停止服务
docker-compose down

# 重启服务
docker-compose restart

# 查看日志
docker-compose logs ikuai-komari-agent

# 进入容器调试
docker-compose exec ikuai-komari-agent /bin/bash
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
├── config.py                # 配置文件
├── requirements.txt         # Python依赖
├── Dockerfile              # Docker构建文件
├── docker-compose.yml      # Docker Compose配置
├── .dockerignore          # Docker忽略文件
├── logs/                  # 日志目录（自动创建）
└── README.md              # 说明文档
```

## 🔧 传统部署方式

如果你不想使用Docker，也可以使用传统方式部署：

### 安装文档

[传统安装文档](Install.md)

### 服务管理

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
```

## 🐛 故障排除

### Docker部署问题

1. **容器无法启动**
```bash
# 查看详细错误信息
docker-compose logs ikuai-komari-agent

# 检查配置文件
cat config.py
```

2. **网络连接问题**
```bash
# 进入容器测试网络
docker-compose exec ikuai-komari-agent /bin/bash
ping your-ikuai-router-ip
```

3. **权限问题**
```bash
# 检查日志目录权限
ls -la logs/
chmod 755 logs/
```

### 配置问题

- 确保iKuai路由器地址可访问
- 检查用户名密码是否正确
- 验证Komari服务器地址和令牌

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## ⭐ 星标

如果这个项目对您有帮助，请给它一个星标 ⭐

---

**注意**: Docker部署方式更加简单可靠，推荐使用Docker进行部署。