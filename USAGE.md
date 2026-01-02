# TradingAgents-CN 使用指南

本文档汇总了 TradingAgents-CN 的 Docker 部署与访问方法，方便您快速上手。

## 1. 🚀 Docker 快速启动

### 准备工作
1. 确保已安装 [Docker Desktop](https://www.docker.com/products/docker-desktop/)。
2. 复制配置文件模板：
   ```bash
   cp .env.docker .env
   ```
3. 编辑 `.env` 文件，填入您的 API 密钥（如 `DEEPSEEK_API_KEY`、`TUSHARE_TOKEN`）。

### 启动命令

**方法 A：标准 Docker 命令（推荐）**
```bash
# 首次启动或代码更新后（重新构建镜像）
docker-compose up -d --build

# 日常启动（使用现有镜像）
docker-compose up -d
```

**方法 B：智能启动脚本**
脚本会自动检测代码变更并决定是否需要重新构建。
- **Mac/Linux**:
  ```bash
  chmod +x scripts/smart_start.sh
  ./scripts/smart_start.sh
  ```
- **Windows**:
  ```powershell
  .\scripts\smart_start.ps1
  ```

### 常用维护命令
```bash
# 查看所有服务日志
docker-compose logs -f

# 查看特定服务日志
docker-compose logs -f backend
docker-compose logs -f frontend

# 停止服务
docker-compose down

# 检查服务状态
docker-compose ps
```

---

## 2. 🌐 访问项目

启动成功后（看到 `healthy` 状态），可以通过以下方式访问：

### 🖥️ Web 可视化界面（主要入口）
- **地址**: [http://localhost:3000](http://localhost:3000)
- **功能**: 
    - 股票全方位分析报告
    - 可视化配置管理
    - 历史记录查看

### 🔌 后端 API 文档（开发调试）
- **Swagger UI**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **ReDoc**: [http://localhost:8000/redoc](http://localhost:8000/redoc)

### ⌨️ 命令行工具 (CLI)
在 Docker 容器内运行命令行工具：

```bash
# 进入交互式 CLI 菜单
docker-compose exec backend python -m cli.main

# 直接分析特定股票（例如 NVDA）
docker-compose exec backend python -m cli.main --ticker NVDA
```

---

## 3. ❓ 常见问题排查

- **服务无法启动？**
    - 检查端口占用：确保 3000 (前端) 和 8000 (后端) 端口未被其他程序占用。
    - 检查 `.env` 配置：确保 API Key 格式正确且没有多余空格。

- **更多帮助**
    - 运行排查脚本 (Mac/Linux): `./scripts/debug_docker.sh`
    - 查看详细文档: `docs/docker/startup-guide.md`
