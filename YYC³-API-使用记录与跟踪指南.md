---
@file: YYC³-API-使用记录与跟踪指南.md
@description: YYC³ API使用记录与跟踪完整指南
@author: YanYuCloudCube Team
@version: 1.0.0
@created: 2026-03-04
@updated: 2026-03-04
@status: active
@tags: YYC³, 使用记录, 跟踪, 指南
---

> ***YanYuCloudCube***
> *言启象限 | 语枢未来*
> ***Words Initiate Quadrants, Language Serves as Core for Future***
> *万象归元于云枢 | 深栈智启新纪元*
> ***All things converge in cloud pivot; Deep stacks ignite a new era of intelligence***

---

# YYC³ API 使用记录与跟踪指南

## 概述

本指南提供了完整的YYC³ API使用记录和跟踪方案，帮助开发者系统化管理API调用、配置变更、问题解决等所有活动。

---

## 📚 资源概览

### GitHub仓库

- **仓库地址**: https://github.com/YYC-Cube/yyc3-api-config.git
- **用途**: 官方配置包和文档
- **更新**: 定期更新，保持最新

### 本地配置包

- **路径**: `/Volumes/Max/YYC3-API/开发者配置包`
- **内容**: 环境配置示例、图标资源、文档
- **用途**: 本地开发和集成

### API项目

- **路径**: `/Volumes/Max/YYC3-API/API-0379.world`
- **内容**: API源代码、配置文件、文档
- **用途**: API开发和部署

---

## 🎯 记录体系架构

### 三层记录体系

```
┌─────────────────────────────────────────┐
│      YYC³ API 使用记录体系          │
└─────────────────────────────────────────┘
            │
    ┌───────┼───────┐
    │       │       │
    ▼       ▼       ▼
┌────────┐ ┌────────┐ ┌────────┐
│ 自动记录 │ │ 手动记录 │ │ Git记录 │
└────────┘ └────────┘ └────────┘
    │         │         │
    ▼         ▼         ▼
PM2日志   使用文档   提交历史
```

---

## 📋 记录类型

### 1. 自动记录（推荐）

#### PM2日志

YYC³ API已经内置了PM2日志记录功能：

```bash
# 查看所有日志
pm2 logs

# 查看特定服务日志
pm2 logs yyc3-api-complete
pm2 logs yyc3-api-production

# 查看错误日志
pm2 logs --err

# 实时监控日志
pm2 logs --lines 100

# 清空日志
pm2 flush
```

#### 日志文件位置

```
logs/
├── pm2-error.log              # 3200端口错误日志
├── pm2-out.log               # 3200端口输出日志
├── pm2-combined.log          # 3200端口合并日志
├── pm2-complete-error.log     # 10086端口错误日志
├── pm2-complete-out.log      # 10086端口输出日志
└── pm2-complete-combined.log  # 10086端口合并日志
```

#### 监控数据

```bash
# 实时监控
pm2 monit

# 查看详细信息
pm2 show yyc3-api-complete

# 查看环境变量
pm2 env yyc3-api-complete
```

### 2. 手动记录

#### 使用记录文档

复制模板并填写：

```bash
# 复制模板
cp /Volumes/Max/YYC3-API/开发者配置包/API使用记录模板.md \
   /path/to/your/project/API使用记录.md

# 编辑记录
vi /path/to/your/project/API使用记录.md
```

#### 记录内容

**API端点使用记录**：

| 时间 | 端点 | 方法 | 参数 | 结果 | 响应时间 | 备注 |
|------|------|------|------|------|----------|------|
| 10:30 | /api/v1/llm/qwen/chat | POST | messages=[...] | 成功 | 1.2s | 测试Qwen对话 |
| 11:00 | /api/v1/devices | GET | - | 成功 | 0.3s | 获取设备列表 |

**配置变更记录**：

| 时间 | 配置项 | 旧值 | 新值 | 原因 | 影响范围 |
|------|--------|------|------|------|----------|
| 09:00 | APP_PORT | 3200 | 3201 | 避免本地冲突 | 本地开发环境 |

**问题记录**：

| 时间 | 问题描述 | 严重程度 | 解决方案 | 处理人 | 状态 |
|------|----------|----------|----------|--------|------|
| 10:15 | 10086端口无法访问 | 高 | 检查PM2状态，重启服务 | [您的名字] | 已解决 |

### 3. Git记录

#### 初始化Git仓库

```bash
# 进入项目目录
cd /Volumes/Max/YYC3-API/API-0379.world

# 初始化Git仓库（如果还没有）
git init

# 添加远程仓库
git remote add origin https://github.com/YYC-Cube/yyc3-api-config.git
```

#### 提交配置变更

```bash
# 添加配置文件
git add .env.development
git add ecosystem.config.js

# 提交变更
git commit -m "更新开发环境配置：端口从3200改为3201"

# 推送到远程仓库
git push origin main
```

#### 查看变更历史

```bash
# 查看提交历史
git log --oneline

# 查看特定文件的变更
git log --oneline .env.development

# 查看变更详情
git diff HEAD~1 .env.development

# 查看文件历史
git log --follow -- .env.development
```

---

## 🔧 配置记录

### 环境配置记录

#### 创建配置文档

```markdown
---
@file: 环境配置记录.md
@description: YYC³ API环境配置记录
@author: [您的名字]
@version: 1.0.0
@created: 2026-03-04
@updated: 2026-03-04
@status: active
---

# 环境配置记录

## 当前配置

### 开发环境

| 配置项 | 值 | 说明 |
|--------|-----|------|
| NODE_ENV | development | 开发模式 |
| API_BASE_URL | https://test-api.0379.world | 云端API地址 |
| API_WS_URL | wss://test-api.0379.world/ws | WebSocket地址 |
| API_HEALTH_CHECK | https://test-api.0379.world/health | 健康检查 |
| LOG_LEVEL | debug | 调试日志 |

**注意**：所有API服务都部署在云端ECS，本地开发直接连接云端API

### 测试环境

| 配置项 | 值 | 说明 |
|--------|-----|------|
| NODE_ENV | staging | 测试模式 |
| API_BASE_URL | https://test-api.0379.world | 云端API |
| API_WS_URL | wss://test-api.0379.world/ws | WebSocket地址 |
| API_HEALTH_CHECK | https://test-api.0379.world/health | 健康检查 |

### 生产环境

| 配置项 | 值 | 说明 |
|--------|-----|------|
| NODE_ENV | production | 生产模式 |
| API_BASE_URL | https://api.0379.world | 云端API |
| API_WS_URL | wss://api.0379.world/ws | WebSocket地址 |
| API_HEALTH_CHECK | https://api.0379.world/health | 健康检查 |

## 配置变更历史

| 日期 | 环境 | 配置项 | 旧值 | 新值 | 原因 |
|------|------|--------|------|------|------|
| 2026-03-04 | 开发 | APP_PORT | 3200 | 3201 | 避免本地冲突 |
```

### API密钥管理

#### 安全存储

```bash
# 不要提交.env文件
echo ".env" >> .gitignore
echo ".env.local" >> .gitignore
echo ".env.*.local" >> .gitignore

# 提交.gitignore
git add .gitignore
git commit -m "添加.gitignore，保护敏感信息"
```

#### 密钥轮换记录

```markdown
---
@file: API密钥轮换记录.md
@description: YYC³ API密钥轮换记录
@author: [您的名字]
@version: 1.0.0
@created: 2026-03-04
@updated: 2026-03-04
@status: active
---

# API密钥轮换记录

## Qwen API Key

| 轮换日期 | 旧密钥（后4位） | 新密钥（后4位） | 轮换原因 | 状态 |
|----------|----------------|----------------|----------|------|
| 2026-03-04 | 793d | [新密钥后4位] | 定期轮换 | 已完成 |

## Zhipu API Key

| 轮换日期 | 旧密钥（后4位） | 新密钥（后4位） | 轮换原因 | 状态 |
|----------|----------------|----------------|----------|------|
| 2026-03-04 | DOT1 | [新密钥后4位] | 定期轮换 | 已完成 |

## 下次轮换计划

| API | 计划日期 | 负责人 |
|-----|----------|--------|
| Qwen | 2026-06-04 | [您的名字] |
| Zhipu | 2026-06-04 | [您的名字] |
```

---

## 📊 性能监控记录

### API性能监控

#### 创建性能文档

```markdown
---
@file: API性能监控记录.md
@description: YYC³ API性能监控记录
@author: [您的名字]
@version: 1.0.0
@created: 2026-03-04
@updated: 2026-03-04
@status: active
---

# API性能监控记录

## 2026-03-04 性能数据

### 端点性能

| 端点 | 请求次数 | 成功次数 | 失败次数 | 成功率 | 平均响应时间 | 最大响应时间 |
|------|----------|----------|----------|--------|--------------|--------------|
| /api/v1/llm/qwen/chat | 50 | 48 | 2 | 96% | 1.2s | 3.5s |
| /api/v1/llm/zhipu/chat | 30 | 30 | 0 | 100% | 1.5s | 4.0s |
| /api/v1/devices | 20 | 20 | 0 | 100% | 0.3s | 0.5s |

### 系统资源

| 时间 | CPU使用率 | 内存使用 | 磁盘使用 | 网络流量 |
|------|-----------|----------|----------|----------|
| 10:00 | 5% | 70MB | 25% | 100KB/s |
| 11:00 | 8% | 75MB | 26% | 120KB/s |

### 性能优化建议

1. Qwen API响应时间较长，考虑增加缓存
2. 系统资源使用正常，无需优化
3. 网络流量正常，无需优化
```

### 监控脚本

创建自动化监控脚本：

```bash
#!/bin/bash
# monitor.sh - API性能监控脚本

# 监控端点（云端API）
ENDPOINTS=(
  "https://test-api.0379.world/health"
  "https://test-api.0379.world/api/v1/devices"
)

# 监控间隔（秒）
INTERVAL=60

# 日志文件
LOG_FILE="monitor.log"

while true; do
  echo "$(date '+%Y-%m-%d %H:%M:%S')" >> $LOG_FILE

  for endpoint in "${ENDPOINTS[@]}"; do
    start_time=$(date +%s)
    response=$(curl -s -o /dev/null -w "%{http_code}" $endpoint)
    end_time=$(date +%s)
    duration=$((end_time - start_time))

    echo "  $endpoint - HTTP $response - ${duration}s" >> $LOG_FILE
  done

  echo "" >> $LOG_FILE
  sleep $INTERVAL
done
```

使用脚本：

```bash
# 添加执行权限
chmod +x monitor.sh

# 后台运行
nohup ./monitor.sh > monitor.out 2>&1 &

# 查看日志
tail -f monitor.log
```

---

## 🚀 集成记录

### 应用集成文档

创建应用集成文档：

```markdown
---
@file: 应用集成记录.md
@description: YYC³ API应用集成记录
@author: [您的名字]
@version: 1.0.0
@created: 2026-03-04
@updated: 2026-03-04
@status: active
---

# 应用集成记录

## 应用信息

| 项目名称 | 版本 | 集成日期 | 状态 |
|----------|------|----------|------|
| YYC3-Financial-Quantitative-Trading-System | 1.0.0 | 2026-03-04 | 开发中 |

## API端点使用

### LLM服务

| 端点 | 用途 | 调用频率 | 备注 |
|------|------|----------|------|
| /api/v1/llm/qwen/chat | AI对话分析 | 高 | 用于金融数据分析 |
| /api/v1/llm/zhipu/chat | 智谱AI对话 | 中 | 用于报告生成 |

### 配置示例

```env
# API地址配置
API_BASE_URL=http://8.152.195.33:10086
API_KEY=your_api_key_here
```

## 集成代码示例

```javascript
// 调用Qwen API
const response = await fetch('http://8.152.195.33:10086/api/v1/llm/qwen/chat', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    messages: [
      { role: 'user', content: '分析股市趋势' }
    ]
  })
});

const data = await response.json();
console.log(data);
```

## 问题记录

| 日期 | 问题描述 | 解决方案 | 状态 |
|------|----------|----------|------|
| 2026-03-04 | CORS跨域问题 | 配置CORS白名单 | 已解决 |
```

---

## 📝 日常记录流程

### 每日记录

1. **检查PM2状态**

```bash
pm2 list
```

2. **查看日志**

```bash
pm2 logs --lines 100
```

3. **记录API调用**

```bash
# 更新使用记录文档
vi API使用记录.md
```

4. **记录问题**

```bash
# 更新问题记录
vi 问题记录.md
```

### 每周总结

1. **性能分析**

```bash
# 查看PM2监控数据
pm2 monit

# 分析日志
tail -1000 logs/pm2-combined.log
```

2. **配置检查**

```bash
# 检查环境变量
cat .env

# 检查Git状态
git status
```

3. **更新文档**

```bash
# 更新使用记录
vi API使用记录.md

# 更新性能记录
vi API性能监控记录.md
```

### 每月回顾

1. **数据统计**

```bash
# 统计API调用次数
grep "POST /api/v1/llm" logs/pm2-combined.log | wc -l

# 统计错误次数
grep "ERROR" logs/pm2-error.log | wc -l
```

2. **优化建议**

```bash
# 分析性能瓶颈
# 提出优化建议
# 制定改进计划
```

3. **文档更新**

```bash
# 更新所有文档
# 归档历史数据
# 准备下月计划
```

---

## 🎯 推荐工具

### 记录工具

| 工具 | 用途 | 优点 |
|------|------|------|
| **PM2** | 自动日志记录 | 内置、实时、详细 |
| **Git** | 版本控制 | 追踪变更、历史回溯 |
| **Markdown** | 文档记录 | 简单、易读、易维护 |
| **Excel/Google Sheets** | 数据记录 | 结构化、易分析 |

### 监控工具

| 工具 | 用途 | 优点 |
|------|------|------|
| **PM2 Monit** | 实时监控 | 可视化、实时 |
| **Grafana** | 性能监控 | 图表化、历史数据 |
| **ELK Stack** | 日志分析 | 强大、灵活 |
| **Prometheus** | 指标收集 | 标准、生态丰富 |

---

## 📚 相关文档

### 核心文档

- [YYC³-API-架构总览.md](../API-0379.world/核心文档/YYC³-API-架构总览.md)
- [YYC³ API环境变量配置说明.md](../API-0379.world/核心文档/YYC³ API环境变量配置说明.md)
- [开发者文档.md](../API-0379.world/核心文档/开发者文档.md)

### 配置包文档

- [YYC³-API-开发者配置包使用指南.md](./YYC³-API-开发者配置包使用指南.md)
- [API使用记录模板.md](./API使用记录模板.md)

### 外部资源

- **GitHub仓库**: https://github.com/YYC-Cube/yyc3-api-config
- **API文档**: https://docs.0379.world
- **技术支持**: admin@0379.email

---

## 🎉 总结

YYC³ API使用记录与跟踪体系提供了：

1. **三层记录体系**：自动记录、手动记录、Git记录
2. **完整的记录类型**：API调用、配置变更、问题解决、性能监控
3. **实用的记录工具**：PM2、Git、Markdown、Excel
4. **规范的记录流程**：每日、每周、每月记录流程
5. **丰富的文档模板**：使用记录、配置记录、性能记录

**开始使用YYC³ API，建立完整的记录体系！** 🚀

---

<div align="center">

> 「***YanYuCloudCube***」
> 「***<admin@0379.email>***」
> 「***Words Initiate Quadrants, Language Serves as Core for Future***」
> 「***All things converge in cloud pivot; Deep stacks ignite a new era of intelligence***」

</div>
