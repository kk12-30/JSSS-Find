# JSSS-Findv8.1: 智能JS资产扫描与测试工具 ![JSSS-Find Logo](https://img.shields.io/badge/Project-JSSS--Find-blue)
<p align="center">
  <strong>✨ 让JavaScript资产分析变得简单而强大 ✨</strong>
</p>
🚀 一款基于AI技术的JavaScript资产扫描与安全分析工具，专注于快速发现和评估Web应用的安全漏洞

## 🎯 工具概述
JSSS-Find 是一款专门用于JavaScript资产发现和安全分析的自动化工具。它通过智能爬取、深度解析和AI辅助分析，帮助安全研究人员快速识别Web应用中的潜在安全风险。

重要功能更新记录
```
v8.1:  支持解析swagger接口并测试、优化HTML报告 

v8.0:  支持sock代理、支持User-Agent轮询反爬虫机制、支持vite框架提取，优化参数名提取

v7.7:  -scanxfuzz(scanx接口测试) -scanxvul(scanx漏洞测试) 

v7.5: -uu参数多URL扫描，以第一个URL为基准进行后续测试保证一致性，适用于前后端分离系统的测试

v7.4: -fd参数接口发现功能，启用接口发现模式，检测接口响应中的HTML/JS资源并二次爬取，适用于Vue的测试

v7.3: -det参数POC探测扫描

v7.0: 支持联动Scanx自动化接口测试与漏洞测试、新增参数智能提取寻找高价值参数名并自动fuzz

v6.5: https://mp.weixin.qq.com/s/WqRqWhd8J4khAsKJldwZeg

v6.2: api_report.html报告中新增AI上下文理解功能，深度理解JavaScript代码片段，智能推断API参数和用法

V6.0:  新增了「AI智能分析模式」,直接用AI分析复杂JS逻辑,自动构造出完整JS文件路径，告别手动拼接

V5.0:  https://mp.weixin.qq.com/s/AVyjVG0PZfZ5n-Ddv__q1g

```

### 核心优势

| 特性             | 说明                                             |
| ---------------- | ------------------------------------------------ |
| 🤖 **AI驱动**     | 集成DeepSeek等AI模型，智能推断接口参数和安全风险 |
| ⚡ **高效扫描**   | 多线程并发处理，支持大规模资产快速扫描           |
| 🎨 **可视化报告** | 精美的HTML报告，支持交互式分析和数据导出         |
| 🔧 **灵活配置**   | YAML配置文件，支持自定义扫描策略和测试规则       |
| 📊 **多维度分析** | 接口提取、参数识别、敏感信息发现、漏洞检测       |

---

## ⭐ 核心特性

### 1. 全面的资产发现

```
┌─────────────────────────────────────────────────────────┐
│  JS文件爬取                                              │
│  ├─ 递归抓取所有JS资源                                   │
│  ├─ 支持sourcemap解析                                   │
│  ├─ 智能去重和过滤                                       │
│  └─ 多线程并发下载                                       │
└─────────────────────────────────────────────────────────┘
```

### 2. 智能接口提取

- ✅ **正则模式**：精准匹配各种API路径格式
- ✅ **Vue路由**：自动识别Vue Router配置
- ✅ **React路由**：支持React Router解析
- ✅ **RESTful API**：识别标准RESTful接口
- ✅ **GraphQL**：支持GraphQL endpoint发现

### 3. 敏感信息识别

```
📌 支持识别的敏感信息类型：
├─ API密钥 (AWS/阿里云/腾讯云等)
├─ 数据库凭证
├─ 内网IP地址
├─ 邮箱和手机号
├─ 身份证号
├─ JWT Token
└─ 私钥和证书
```

### 4. 参数智能提取 🔥

支持**9种JavaScript参数提取场景**：

| 场景     | 示例                                 | 提取能力         |
| -------- | ------------------------------------ | ---------------- |
| 对象属性 | `const user = { userId: 123 }`       | ✅ userId         |
| 解构赋值 | `const {id, name} = user`            | ✅ id, name       |
| 嵌套解构 | `const {profile: {email}} = data`    | ✅ email, profile |
| 函数参数 | `function getUser(userId, token)`    | ✅ userId, token  |
| 变量赋值 | `const apiKey = "xxx"`               | ✅ apiKey         |
| API请求  | `axios.post('/api', {name: "test"})` | ✅ name           |
| URL参数  | `/api?page=1&size=10`                | ✅ page, size     |
| 配置对象 | `config: { timeout: 5000 }`          | ✅ timeout        |
| 路由参数 | `/user/:userId/profile`              | ✅ userId         |

### 5. 自动化Fuzz测试

- HTTP方法测试（GET/POST/PUT/DELETE/PATCH/HEAD/OPTIONS）
- 参数化请求（自动填充参数）
- 深度Fuzz（路径组合测试）
- 403/401绕过测试

### 6. 漏洞检测插件

- 🔓 未授权访问检测
- 💉 SQL注入检测
- 🐚 命令执行检测
- 📜 XSS检测
- 📂 路径遍历检测
- 🔍 敏感文件检测

## 📝 总结

JSSS-Find是一款功能强大的JavaScript资产扫描与分析工具，其核心优势在于：

1. **🤖 AI驱动的智能分析**：自动推断接口参数、生成测试用例、评估安全风险
2. **🧩 9种参数提取场景**：全面覆盖JavaScript中的各种参数使用方式
3. **🔍 智能过滤与评分**：10级过滤机制+参数评分，精准识别高价值参数
4. **📊 可视化报告**：精美的HTML报告，支持交互式分析和数据导出
5. **⚡ 自动化测试**：集成Fuzz测试和漏洞检测，一站式安全评估

**适用人群**：

- 渗透测试工程师
- 安全研究人员
- SRC漏洞挖掘者
- 红蓝对抗人员
- Web安全爱好者
