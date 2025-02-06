# JSSS-Find: 自动化JS提取与漏洞检测工具 ![JSSS-Find Logo](https://img.shields.io/badge/Project-JSSS--Find-blue)

JSSS-Find 是一款用于自动化提取JS文件、API接口测试以及暴露端点检测的工具。通过访问指定URL，提取并分析JS文件中的接口、路径和敏感信息，帮助开发者发现潜在的安全漏洞。该工具支持对网站进行fuzz测试、漏洞检测、真实浏览器中访问Vue接口等功能。适用于安全研究人员和开发者进行漏洞检测与接口审计。
![](https://github.com/kk12-30/JSSS-Find/blob/main/image.png)

## 功能 ![Features Icon](https://img.shields.io/badge/Features-✔️-green)

- **JS文件提取**：从网页内容中自动提取JS文件链接(适用Webpack框架)。
- **接口路径提取**：支持精简和全量接口路径的提取，自动化识别JS中的接口路由。
- **敏感信息提取**：提取JS文件中的敏感信息，如API密钥、JWT令牌、数据库凭证等。
- **Fuzz测试**：对提取的接口路径进行fuzz测试、403bypass，发现潜在的漏洞。
- **漏洞检测**：通过规则检测每个接口的常见漏洞，如Spring Actuator、Swagger未授权等。
- **Vue接口检测**：在真实浏览器环境下测试Vue接口的状态码和标题。


## 使用方法 🚀

### 1. 提取JS文件并分析 📝

#### 访问URL提取JS文件 🌐

```bash
JSSS-Find.exe -u <URL> [-fuzz] [-v] [-vueBrowser]
```

- `-u <URL>`: 指定需要提取JS文件和进行测试的URL。
- `-fuzz`: 启用fuzz测试。
- `-v`: 启用漏洞检测模式，速度较慢。
- `-vueBrowser`: 在真实浏览器环境中访问Vue接口。

#### 读取本地JS文件目录 📂

```bash
JSSS-Find.exe -f <本地JS目录> [-fuzz] [-v] [-vueBrowser]
```

- `-f <本地JS目录>`: 指定本地目录，工具会自动分析该目录下的所有JS文件。

### 2. 通过Cookie和Header进行请求 🍪

#### 设置自定义的Cookie和Headers 🔑

```bash
JSSS-Find.exe -u <URL> -cookie "SESSIONID=abcd" -header "Token:abc;User-Agent:MyUA"
```

- `-cookie`: 设置自定义Cookie。
- `-header`: 设置自定义请求Headers。

### 3. 保存和查看结果 💾

工具会在指定的目录中保存提取结果，包括：

- `精简正则接口提取.txt`
- `全量正则接口提取.txt`
- `敏感信息提取.txt`
- `fuzz_success.txt` (仅在启用fuzz时生成)
- `vuln_result.txt` (仅在启用漏洞检测时生成)
- `vue_browser_result.txt` (仅在启用Vue浏览器检测时生成)

## 示例 ⚡

```bash
JSSS-Find.exe -u https://example.com -fuzz -v
```

上述命令会从 `https://example.com` 提取JS文件、进行接口fuzz测试，并检测常见漏洞。

