---
@file: config.example.js
@description: YYC³ API Configuration Usage Examples
@author: YanYuCloudCube Team
@version: 1.0.0
@created: 2026-03-02
@updated: 2026-03-02
@status: active
@tags: [configuration],[examples],[Node.js]
---

> ***YanYuCloudCube***
> *Words Initiate Quadrants, Language Serves as Core for Future*
> *All things converge in cloud pivot; Deep stacks ignite a new era of intelligence*

---

# YYC³ API Configuration Examples

## Overview

This document provides complete example code for using YYC³ API configuration.

**Language**: Node.js  
**API Version**: 2.0.0

---

## 🚀 Quick Start

### 1. Install Dependencies

```bash
npm install dotenv axios
```

### 2. Create Configuration File

```javascript
const config = require('dotenv').config();

if (config.error) {
  throw config.error;
}

module.exports = {
  env: process.env.NODE_ENV,
  api: {
    baseUrl: process.env.API_BASE_URL,
    healthCheck: process.env.API_HEALTH_CHECK,
    wsUrl: process.env.API_WS_URL
  },
  llm: {
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
  },
  jwt: {
    secret: process.env.JWT_SECRET,
    expiresIn: process.env.JWT_EXPIRES_IN
  },
  redis: {
    host: process.env.REDIS_HOST,
    port: process.env.REDIS_PORT,
    password: process.env.REDIS_PASSWORD,
    db: process.env.REDIS_DB
  },
  logging: {
    level: process.env.LOG_LEVEL,
    file: process.env.LOG_FILE
  }
};
```

### 3. Use Configuration

```javascript
const config = require('./config');

console.log('Environment:', config.env);
console.log('API Base URL:', config.api.baseUrl);
```

---

## 📋 Complete Examples

### Example 1: Basic API Call

```javascript
require('dotenv').config();
const axios = require('axios');

const apiClient = axios.create({
  baseURL: process.env.API_BASE_URL,
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

### Example 2: Call Qwen API

```javascript
require('dotenv').config();
const axios = require('axios');

const apiClient = axios.create({
  baseURL: process.env.API_BASE_URL,
  headers: {
    'Content-Type': 'application/json'
  }
});

async function chatWithQwen(message) {
  try {
    const response = await apiClient.post('/api/v1/llm/qwen/chat', {
      messages: [{ role: 'user', content: message }]
    });
    console.log('Response:', response.data);
    return response.data;
  } catch (error) {
    console.error('Chat failed:', error.message);
    throw error;
  }
}

chatWithQwen('Hello, please introduce the YYC³ project');
```

### Example 3: Get Device List

```javascript
require('dotenv').config();
const axios = require('axios');

const apiClient = axios.create({
  baseURL: process.env.API_BASE_URL,
  headers: {
    'Content-Type': 'application/json'
  }
});

async function getDevices() {
  try {
    const response = await apiClient.get('/api/v1/devices');
    console.log('Devices:', response.data);
    return response.data;
  } catch (error) {
    console.error('Get devices failed:', error.message);
    throw error;
  }
}

getDevices();
```

### Example 4: WebSocket Connection

```javascript
require('dotenv').config();
const WebSocket = require('ws');

const ws = new WebSocket(process.env.API_WS_URL);

ws.on('open', () => {
  console.log('WebSocket connected');
  ws.send(JSON.stringify({ type: 'ping' }));
});

ws.on('message', (data) => {
  console.log('Received:', data.toString());
});

ws.on('error', (error) => {
  console.error('WebSocket error:', error);
});

ws.on('close', () => {
  console.log('WebSocket disconnected');
});
```

### Example 5: Complete API Client Class

```javascript
require('dotenv').config();
const axios = require('axios');

class YYC3APIClient {
  constructor() {
    this.client = axios.create({
      baseURL: process.env.API_BASE_URL,
      headers: {
        'Content-Type': 'application/json'
      }
    });
  }

  async healthCheck() {
    const response = await this.client.get('/health');
    return response.data;
  }

  async chatWithQwen(messages) {
    const response = await this.client.post('/api/v1/llm/qwen/chat', {
      messages
    });
    return response.data;
  }

  async chatWithZhipu(messages) {
    const response = await this.client.post('/api/v1/llm/zhipu/chat', {
      messages
    });
    return response.data;
  }

  async chatWithOllama(messages) {
    const response = await this.client.post('/api/v1/llm/ollama/chat', {
      messages
    });
    return response.data;
  }

  async getDevices() {
    const response = await this.client.get('/api/v1/devices');
    return response.data;
  }

  async getDevice(deviceId) {
    const response = await this.client.get(`/api/v1/devices/${deviceId}`);
    return response.data;
  }

  async controlDevice(deviceId, command) {
    const response = await this.client.post(`/api/v1/devices/${deviceId}/control`, {
      command
    });
    return response.data;
  }

  async getDeviceStatus(deviceId) {
    const response = await this.client.get(`/api/v1/devices/${deviceId}/status`);
    return response.data;
  }

  async getSystemStatus() {
    const response = await this.client.get('/api/v1/status');
    return response.data;
  }

  async getAvailableModels() {
    const response = await this.client.get('/api/v1/llm/models');
    return response.data;
  }
}

const api = new YYC3APIClient();

async function test() {
  try {
    const health = await api.healthCheck();
    console.log('Health check:', health);

    const chat = await api.chatWithQwen([{ role: 'user', content: 'Hello' }]);
    console.log('Chat response:', chat);

    const devices = await api.getDevices();
    console.log('Devices:', devices);
  } catch (error) {
    console.error('Error:', error.message);
  }
}

test();
```

---

## 🔧 Advanced Configuration

### Configuration Validation

```javascript
require('dotenv').config();

const requiredEnvVars = [
  'NODE_ENV',
  'API_BASE_URL',
  'QWEN_API_KEY',
  'ZHIPU_API_KEY'
];

const missing = requiredEnvVars.filter(varName => !process.env[varName]);

if (missing.length > 0) {
  throw new Error(`Missing required environment variables: ${missing.join(', ')}`);
}

console.log('All required environment variables are set');
```

### Environment Detection

```javascript
require('dotenv').config();

const isDevelopment = process.env.NODE_ENV === 'development';
const isStaging = process.env.NODE_ENV === 'staging';
const isProduction = process.env.NODE_ENV === 'production';

if (isDevelopment) {
  console.log('Running in development mode');
} else if (isStaging) {
  console.log('Running in staging mode');
} else if (isProduction) {
  console.log('Running in production mode');
} else {
  console.warn('Unknown environment:', process.env.NODE_ENV);
}
```

### Configuration Switching

```javascript
const fs = require('fs');
const path = require('path');

function loadConfig(env) {
  const envFile = `.env.${env}`;
  const envPath = path.join(__dirname, envFile);

  if (!fs.existsSync(envPath)) {
    throw new Error(`Environment file not found: ${envFile}`);
  }

  require('dotenv').config({ path: envPath });
  console.log(`Loaded configuration for ${env} environment`);
}

loadConfig('development');
```

---

## 📚 Related Documentation

- [README.md](./README.md) - Configuration package usage guide
- [.env.development](./.env.development) - Development environment configuration
- [.env.staging](./.env.staging) - Staging environment configuration

---

<div align="center">

> ***YanYuCloudCube***
> ***Words Initiate Quadrants, Language Serves as Core for Future***
> ***All things converge in cloud pivot; Deep stacks ignite a new era of intelligence***

**YYC³ API Configuration Examples**

**Version**: 1.0.0  
**API Version**: 2.0.0

</div>
