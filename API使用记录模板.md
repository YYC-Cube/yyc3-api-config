---
@file: API使用记录模板.md
@description: YYC³ API使用记录模板
@author: YanYuCloudCube Team
@version: 1.0.0
@created: 2026-03-04
@updated: 2026-03-04
@status: active
@tags: YYC³, 使用记录, 模板
---

> ***YanYuCloudCube***
> *言启象限 | 语枢未来*
> ***Words Initiate Quadrants, Language Serves as Core for Future***
> *万象归元于云枢 | 深栈智启新纪元*
> ***All things converge in cloud pivot; Deep stacks ignite a new era of intelligence***

---

# YYC³ API 使用记录模板

## 项目信息

| 项目名称 | 版本 | 集成日期 | 状态 |
|----------|------|----------|------|
| [您的项目名称] | [版本号] | 2026-03-04 | 开发中 |

---

## API端点使用记录

### 2026-03-04

| 时间 | 端点 | 方法 | 参数 | 结果 | 响应时间 | 备注 |
|------|------|------|------|------|----------|------|
| 10:30 | /api/v1/llm/qwen/chat | POST | messages=[...] | 成功 | 1.2s | 测试Qwen对话 |
| 11:00 | /api/v1/devices | GET | - | 成功 | 0.3s | 获取设备列表 |
| 11:15 | /api/v1/llm/zhipu/chat | POST | messages=[...] | 成功 | 1.5s | 测试智谱对话 |

---

## 配置变更记录

### 2026-03-04

| 时间 | 配置项 | 旧值 | 新值 | 原因 | 影响范围 |
|------|--------|------|------|------|----------|
| 09:00 | APP_PORT | 3200 | 3201 | 避免本地冲突 | 本地开发环境 |
| 09:30 | LOG_LEVEL | info | debug | 开发调试需要 | 日志输出 |
| 10:00 | CORS_ORIGIN | http://localhost:3000 | http://localhost:3000,http://localhost:5173 | 添加前端支持 | 跨域访问 |

---

## 问题记录与解决方案

### 2026-03-04

| 时间 | 问题描述 | 严重程度 | 解决方案 | 处理人 | 状态 |
|------|----------|----------|----------|--------|------|
| 10:15 | 10086端口无法访问 | 高 | 检查PM2状态，重启服务 | [您的名字] | 已解决 |
| 11:30 | CORS跨域错误 | 中 | 更新CORS_ORIGIN配置 | [您的名字] | 已解决 |
| 14:00 | API响应超时 | 低 | 增加REQUEST_TIMEOUT配置 | [您的名字] | 已解决 |

---

## 性能监控记录

### 2026-03-04

| 时间 | API端点 | 请求次数 | 成功次数 | 失败次数 | 平均响应时间 | 最大响应时间 |
|------|----------|----------|----------|----------|--------------|--------------|
| 10:00 | /api/v1/llm/qwen/chat | 50 | 48 | 2 | 1.2s | 3.5s |
| 11:00 | /api/v1/devices | 20 | 20 | 0 | 0.3s | 0.5s |

---

## 集成代码示例

### Node.js

```javascript
require('dotenv').config();
const axios = require('axios');

const apiClient = axios.create({
  baseURL: process.env.API_BASE_URL,
  headers: {
    'Content-Type': 'application/json'
  }
});

// Qwen对话
async function chatWithQwen(message) {
  try {
    const response = await apiClient.post('/api/v1/llm/qwen/chat', {
      messages: [
        { role: 'user', content: message }
      ]
    });
    return response.data;
  } catch (error) {
    console.error('Error:', error.message);
    throw error;
  }
}

// 使用示例
chatWithQwen('你好')
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

### Python

```python
import os
from dotenv import load_dotenv
import requests

load_dotenv()

API_BASE_URL = os.getenv('API_BASE_URL')

def chat_with_qwen(message):
    try:
        response = requests.post(
            f'{API_BASE_URL}/api/v1/llm/qwen/chat',
            json={
                'messages': [
                    {'role': 'user', 'content': message}
                ]
            }
        )
        return response.json()
    except Exception as error:
        print(f'Error: {error}')
        raise

# 使用示例
data = chat_with_qwen('你好')
print(data)
```

---

## 测试用例记录

### 功能测试

| 测试用例 | 测试端点 | 测试数据 | 预期结果 | 实际结果 | 状态 |
|----------|----------|----------|----------|----------|------|
| Qwen对话 | /api/v1/llm/qwen/chat | messages=[{role:"user",content:"你好"}] | 返回AI回复 | 返回AI回复 | ✅ 通过 |
| 设备列表 | /api/v1/devices | - | 返回设备数组 | 返回设备数组 | ✅ 通过 |
| 健康检查 | /health | - | status="ok" | status="ok" | ✅ 通过 |

---

## 部署记录

### 环境配置

| 环境 | 服务器 | 端口 | 部署日期 | 部署人 | 状态 |
|------|--------|------|----------|--------|------|
| 开发环境 | localhost | 3201 | 2026-03-04 | [您的名字] | 运行中 |
| 测试环境 | test-api.0379.world | 3200 | - | - | 待部署 |
| 生产环境 | api.0379.world | 3200 | - | - | 待部署 |

### 部署步骤

```bash
# 1. 选择环境配置
cp .env.development .env

# 2. 安装依赖
npm install

# 3. 启动服务
npm run dev

# 4. 验证服务
curl http://localhost:3201/health
```

---

## Git提交记录

### 提交历史

| 提交ID | 日期 | 提交信息 | 提交人 |
|--------|------|----------|--------|
| abc123 | 2026-03-04 09:00 | feat: 添加Qwen API集成 | [您的名字] |
| def456 | 2026-03-04 10:00 | fix: 修复CORS配置 | [您的名字] |

### 常用Git命令

```bash
# 查看提交历史
git log --oneline

# 查看变更
git diff

# 添加文件
git add .

# 提交变更
git commit -m "描述变更内容"

# 推送到远程
git push origin main
```

---

## 联系与支持

### 技术支持

- **邮箱**: admin@0379.email
- **文档**: https://docs.0379.world
- **GitHub**: https://github.com/YYC-Cube/yyc3-api-config

### API端点

| 环境 | 地址 | 说明 |
|------|------|------|
| 开发环境 | https://test-api.0379.world | 云端API |
| 测试环境 | https://test-api.0379.world | 云端API |
| 生产环境 | https://api.0379.world | 云端API |

---

## 备注与总结

### 重要提醒

1. **API密钥安全**：不要将`.env`文件提交到公共仓库
2. **环境隔离**：开发、测试、生产环境使用不同的配置
3. **定期备份**：定期备份配置文件和代码
4. **版本控制**：使用Git管理代码变更
5. **日志记录**：记录API调用和问题解决过程

### 下一步计划

- [ ] 完成所有API端点的集成
- [ ] 编写单元测试
- [ ] 部署到测试环境
- [ ] 性能优化
- [ ] 文档完善

---

<div align="center">

**YYC³ API 使用记录模板**

*言启象限 | 语枢未来*

**日期**: 2026-03-04

</div>
