---
@file: YYC³-API-开发者配置包使用指南.md
@description: YYC³ API开发者配置包使用指南
@author: YanYuCloudCube Team
@version: 1.0.0
@created: 2026-03-04
@updated: 2026-03-04
@status: active
@tags: YYC³, 配置包, 使用指南
---

> ***YanYuCloudCube***
> *言启象限 | 语枢未来*
> ***Words Initiate Quadrants, Language Serves as Core for Future***
> *万象归元于云枢 | 深栈智启新纪元*
> ***All things converge in cloud pivot; Deep stacks ignite a new era of intelligence***

---

# YYC³ API 开发者配置包使用指南

## 概述

YYC³ API开发者配置包提供了完整的环境配置、文档和资源，帮助开发者快速集成YYC³ API网关。

---

## 📦 配置包结构

### GitHub仓库
- **仓库地址**: https://github.com/YYC-Cube/yyc3-api-config.git
- **版本**: 1.0.0
- **许可证**: MIT

### 本地配置包
- **路径**: `/Volumes/Max/YYC3-API/开发者配置包`
- **内容**: 环境配置示例、图标资源、文档

---

## 🚀 快速开始

### 1. 获取配置包

#### 从GitHub获取（推荐）

```bash
# 克隆仓库
git clone https://github.com/YYC-Cube/yyc3-api-config.git

# 进入目录
cd yyc3-api-config
```

#### 使用本地配置包

```bash
# 进入本地配置包目录
cd /Volumes/Max/YYC3-API/开发者配置包
```

### 2. 选择环境配置

```bash
# 开发环境
cp .env.development .env

# 测试环境
cp .env.staging .env

# 生产环境（需要单独配置）
cp .env.production .env
```

### 3. 填写API密钥

编辑 `.env` 文件，填写真实的API密钥：

```bash
# 使用文本编辑器打开
vi .env

# 或使用VS Code
code .env
```

**必填配置项**：

```env
# Qwen API Key
QWEN_API_KEY=sk-af9aab1ac5084e0e91476def190f793d

# Zhipu API Key
ZHIPU_API_KEY=235424a273ab40c387e8e3a2571031b7.R5lXPtxc3SCHDOT1
```

---

## 📋 环境配置对比

### 开发环境

| 配置项 | 值 | 说明 |
|--------|-----|------|
| `NODE_ENV` | development | 开发模式 |
| `API_BASE_URL` | https://test-api.0379.world | 云端API地址 |
| `API_WS_URL` | wss://test-api.0379.world/ws | WebSocket地址 |
| `API_HEALTH_CHECK` | https://test-api.0379.world/health | 健康检查 |
| `LOG_LEVEL` | debug | 调试日志 |
| `DEBUG` | true | 启用调试 |

**使用场景**：
- 本地开发
- 功能测试
- API调试

**注意**：所有API服务都部署在云端ECS，本地开发直接连接云端API

### 测试环境

| 配置项 | 值 | 说明 |
|--------|-----|------|
| `NODE_ENV` | staging | 测试模式 |
| `APP_PORT` | 3200 | 测试端口 |
| `API_BASE_URL` | https://test-api.0379.world | 测试API |
| `LOG_LEVEL` | info | 信息日志 |
| `DEBUG` | false | 关闭调试 |
| `ENABLE_SWAGGER` | true | 启用API文档 |

**使用场景**：
- 集成测试
- 预发布验证
- 性能测试

### 生产环境

| 配置项 | 值 | 说明 |
|--------|-----|------|
| `NODE_ENV` | production | 生产模式 |
| `APP_PORT` | 3200 | 生产端口 |
| `API_BASE_URL` | https://api.0379.world | 生产API |
| `LOG_LEVEL` | warn | 警告日志 |
| `DEBUG` | false | 关闭调试 |
| `ENABLE_SWAGGER` | false | 关闭API文档 |

**使用场景**：
- 正式上线
- 生产环境运行
- 用户访问

---

## 🔧 配置项详解

### 核心配置

```env
# 应用配置
NODE_ENV=development           # 环境模式
APP_NAME=yyc3_aify           # 应用名称
APP_VERSION=2.0.0           # 应用版本

# API配置（云端ECS）
API_BASE_URL=https://test-api.0379.world
API_HEALTH_CHECK=https://test-api.0379.world/health
API_WS_URL=wss://test-api.0379.world/ws
```

### AI服务配置

```env
# Qwen AI
QWEN_API_KEY=your_qwen_api_key_here
QWEN_API_BASE=https://dashscope.aliyuncs.com/compatible-mode/v1
QWEN_MODEL=qwen2.5-72b-instruct

# Zhipu AI
ZHIPU_API_KEY=your_zhipu_api_key_here
ZHIPU_API_BASE=https://open.bigmodel.cn/api/paas/v4
ZHIPU_MODEL=glm-4

# Ollama
OLLAMA_API_BASE=http://localhost:11434
OLLAMA_MODEL=llama2
```

### 安全配置

```env
# JWT配置
JWT_SECRET=dev_jwt_secret_key_for_testing_only_not_secure
JWT_EXPIRES_IN=24h
JWT_ALGORITHM=HS256

# CORS配置
CORS_ENABLED=true
CORS_ORIGIN=http://localhost:3000,http://localhost:5173
CORS_METHODS=GET,POST,PUT,DELETE,OPTIONS,PATCH
```

---

## 💡 使用示例

### Node.js项目

#### 1. 安装依赖

```bash
npm install dotenv axios
```

#### 2. 创建配置文件

```javascript
// config.js
require('dotenv').config();

module.exports = {
  api: {
    baseUrl: process.env.API_BASE_URL,
    healthCheck: process.env.API_HEALTH_CHECK,
    wsUrl: process.env.API_WS_URL
  },
  ai: {
    qwen: {
      apiKey: process.env.QWEN_API_KEY,
      apiBase: process.env.QWEN_API_BASE,
      model: process.env.QWEN_MODEL
    },
    zhipu: {
      apiKey: process.env.ZHIPU_API_KEY,
      apiBase: process.env.ZHIPU_API_BASE,
      model: process.env.ZHIPU_MODEL
    }
  }
};
```

#### 3. 使用配置

```javascript
const config = require('./config');
const axios = require('axios');

const apiClient = axios.create({
  baseURL: config.api.baseUrl,
  headers: {
    'Content-Type': 'application/json'
  }
});

async function healthCheck() {
  try {
    const response = await apiClient.get('/health');
    console.log('Health check:', response.data);
    return response.data;
  } catch (error) {
    console.error('Health check failed:', error.message);
    throw error;
  }
}

healthCheck();
```

### Python项目

#### 1. 安装依赖

```bash
pip install python-dotenv requests
```

#### 2. 创建配置文件

```python
# config.py
import os
from dotenv import load_dotenv

load_dotenv()

class Config:
    API_BASE_URL = os.getenv('API_BASE_URL')
    API_HEALTH_CHECK = os.getenv('API_HEALTH_CHECK')
    API_WS_URL = os.getenv('API_WS_URL')

    QWEN_API_KEY = os.getenv('QWEN_API_KEY')
    QWEN_API_BASE = os.getenv('QWEN_API_BASE')
    QWEN_MODEL = os.getenv('QWEN_MODEL')

    ZHIPU_API_KEY = os.getenv('ZHIPU_API_KEY')
    ZHIPU_API_BASE = os.getenv('ZHIPU_API_BASE')
    ZHIPU_MODEL = os.getenv('ZHIPU_MODEL')

config = Config()
```

#### 3. 使用配置

```python
import requests
from config import config

def health_check():
    try:
        response = requests.get(config.API_HEALTH_CHECK)
        print('Health check:', response.json())
        return response.json()
    except Exception as error:
        print('Error:', str(error))
        raise

health_check()
```

---

## 📊 API调用示例

### 健康检查

```bash
# 加载环境变量
source .env

# 健康检查
curl $API_BASE_URL/health
```

### Qwen对话

```bash
curl -X POST $API_BASE_URL/api/v1/llm/qwen/chat \
  -H "Content-Type: application/json" \
  -d '{
    "messages": [
      {"role": "user", "content": "你好"}
    ]
  }'
```

### Zhipu对话

```bash
curl -X POST $API_BASE_URL/api/v1/llm/zhipu/chat \
  -H "Content-Type: application/json" \
  -d '{
    "messages": [
      {"role": "user", "content": "介绍YYC³"}
    ]
  }'
```

### 设备列表

```bash
curl $API_BASE_URL/api/v1/devices
```

---

## 🔒 安全最佳实践

### 1. 保护敏感信息

```bash
# .gitignore
.env
.env.local
.env.*.local
*.log
node_modules/
```

### 2. 使用环境变量

```javascript
// ❌ 错误：硬编码
const API_KEY = 'sk-af9aab1ac5084e0e91476def190f793d';

// ✅ 正确：使用环境变量
const API_KEY = process.env.QWEN_API_KEY;
```

### 3. API密钥管理

- ✅ 不要在代码中硬编码API密钥
- ✅ 不要将`.env`文件提交到公共仓库
- ✅ 定期轮换API密钥
- ✅ 遵循最小权限原则

---

## 🔄 环境切换

### 切换到开发环境

```bash
# 复制开发配置
cp .env.development .env

# 重启应用
npm run dev
```

### 切换到测试环境

```bash
# 复制测试配置
cp .env.staging .env

# 重启应用
npm run test
```

### 切换到生产环境

```bash
# 复制生产配置
cp .env.production .env

# 重启应用
npm run start
```

---

## 📝 记录使用

### 创建使用记录文档

创建 `API使用记录.md`：

```markdown
---
@file: API使用记录.md
@description: YYC³ API使用记录
@author: [您的名字]
@version: 1.0.0
@created: 2026-03-04
@updated: 2026-03-04
@status: active
---

# API使用记录

## 2026-03-04

### 使用的API端点

| 时间 | 端点 | 方法 | 参数 | 结果 | 备注 |
|------|------|------|------|------|------|
| 10:30 | /api/v1/llm/qwen/chat | POST | messages=[...] | 成功 | 测试Qwen对话 |
| 11:00 | /api/v1/devices | GET | - | 成功 | 获取设备列表 |

### 配置变更

| 时间 | 配置项 | 旧值 | 新值 | 原因 |
|------|--------|------|------|------|
| 09:00 | PORT | 3200 | 3201 | 避免本地冲突 |

### 问题记录

| 时间 | 问题描述 | 解决方案 | 状态 |
|------|----------|----------|------|
| 10:15 | 10086端口无法访问 | 检查PM2状态，重启服务 | 已解决 |
```

### 使用Git记录

```bash
# 初始化Git仓库
git init

# 添加配置文件
git add .env.example

# 提交变更
git commit -m "更新配置：添加Qwen API密钥"

# 查看变更历史
git log --oneline
```

---

## 📚 相关资源

### 文档

- [YYC³-API-架构总览.md](../API-0379.world/核心文档/YYC³-API-架构总览.md)
- [YYC³ API环境变量配置说明.md](../API-0379.world/核心文档/YYC³ API环境变量配置说明.md)
- [开发者文档.md](../API-0379.world/核心文档/开发者文档.md)

### API端点

| 环境 | 地址 | 说明 |
|------|------|------|
| 开发环境 | https://test-api.0379.world | 云端API |
| 测试环境 | https://test-api.0379.world | 云端API |
| 生产环境 | https://api.0379.world | 云端API |

### 联系方式

- **邮箱**: admin@0379.email
- **GitHub**: https://github.com/YYC-Cube/yyc3-api-config
- **文档**: https://docs.0379.world

---

## 🎯 常见问题

### Q1: 如何获取API密钥？

**A**: 访问对应的AI平台注册并获取API密钥：
- Qwen: https://dashscope.aliyuncs.com/
- Zhipu: https://open.bigmodel.cn/

### Q2: 如何测试API连接？

**A**: 使用健康检查端点：

```bash
curl $API_BASE_URL/health
```

### Q3: 如何切换环境？

**A**: 复制对应的配置文件：

```bash
cp .env.development .env  # 开发环境
cp .env.staging .env     # 测试环境
```

### Q4: 如何处理CORS错误？

**A**: 检查CORS配置：

```env
CORS_ORIGIN=http://localhost:3000,http://localhost:5173
```

---

## 🎉 总结

YYC³ API开发者配置包提供了：

1. **完整的环境配置**：开发、测试、生产环境
2. **详细的文档**：使用指南、API文档、示例代码
3. **丰富的资源**：图标、图片、配置模板
4. **安全配置**：API密钥管理、CORS配置
5. **易于集成**：简单配置即可使用

**开始使用YYC³ API，快速构建您的AI应用！** 🚀

---

<div align="center">

> 「***YanYuCloudCube***」
> 「***<admin@0379.email>***」
> 「***Words Initiate Quadrants, Language Serves as Core for Future***」
> 「***All things converge in cloud pivot; Deep stacks ignite a new era of intelligence***」

</div>
