# JSSS-Find: 自动化JS提取与漏洞检测工具 ![JSSS-Find Logo](https://img.shields.io/badge/Project-JSSS--Find-blue)


⚡https://mp.weixin.qq.com/s/di583ERkAc1HFSpQDfk_mw

更新记录

V3.7.0：自定义fuzz规则：fuzz的配置信息fuzzconfig.yaml可自定义

V3.6.3：修复fuzz报告的各种问题

V3.6.0：使用AI进行JS代码审计并自动构造请求包进行测试

V3.5.4：添加了两个参数
-filter int过滤重复响应的阈值，超过此数量的相同大小响应将被过滤 (default 6)
-fuzznum int批量检测时，每个URL的精简接口数量阈值，超过该值则跳过fuzz测试，0表示无限制

V3.5.1：新增-t参数控制并发线程，不加参数默认50

V3.5：支持批量URL扫描，优化报告模板

V3.4：代码重构使用高并发线程，速度提升百分之50

V3.3：修复扫描https的IP地址时证书错误问题


JSSS-Find 是一款用于自动化提取JS文件、API接口测试以及暴露端点检测的工具。通过访问指定URL，提取并分析JS文件中的接口、路径和敏感信息，帮助开发者发现潜在的安全漏洞。该工具支持对网站进行fuzz测试、漏洞检测、真实浏览器中访问Vue接口等功能。适用于安全研究人员和开发者进行漏洞检测与接口审计。

✅提取JS
![](https://github.com/kk12-30/JSSS-Find/blob/main/image.png)
✅AI审计JS，自动化fuzz
![](https://github.com/kk12-30/JSSS-Find/blob/main/ai1.png)
![](https://github.com/kk12-30/JSSS-Find/blob/main/ai2.png)
![](https://github.com/kk12-30/JSSS-Find/blob/main/ai3.png)
✅fuzz测试，支持深度fuzz，自动构造接口
![](https://github.com/kk12-30/JSSS-Find/blob/main/2.png)
✅漏洞检测
![](https://github.com/kk12-30/JSSS-Find/blob/main/3.png)
✅Vue接口检测
![](https://github.com/kk12-30/JSSS-Find/blob/main/4.png)
✅结果保存到本地文件
![](https://github.com/kk12-30/JSSS-Find/blob/main/1.png)
✅报告生成
![](https://github.com/kk12-30/JSSS-Find/blob/main/6.png)


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
-  -m 使用深度fuzz模式，构造大量请求参数进行fuzz（使用方式-fuzz -m）
-  -bypass 会对401/403请求进行绕过测试
- `-v`: 启用漏洞检测模式，速度较慢。
- `-vueBrowser`: 在真实浏览器环境中访问Vue接口。

#### 读取本地JS文件目录 📂

```bash
JSSS-Find.exe -f <本地需要读取的JS目录> [-fuzz] [-v] [-vueBrowser]
```

- `-f <本地JS目录>`: 指定本地目录，工具会自动分析该目录下的所有JS文件。
- `可联动Packer-Fuzzer工具获取的js  该工具下载的js在tmp文件夹中`

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
JSSS-Find.exe -u https://example.com -fuzz -t 10
```
上述命令会从 `https://example.com` 提取JS文件、进行接口fuzz测试、并发速率为10（过大并发可能导致系统崩溃、触发waf等后果）

```bash
JSSS-Find.exe -u https://example.com -fuzz -m -t 10
```
上述命令会从 `https://example.com` 提取JS文件、进行接口fuzz深度测试

```bash
JSSS-Find.exe -ai -clean -u https://example.com
```
上述命令会从 `https://example.com` 提取JS文件、进行AI分析

```bash
JSSS-Find.exe -u https://example.com -fuzz -bypss
```
上述命令会从 `https://example.com` 提取JS文件、进行接口fuzz测试、对403/401请求进行bypass

```bash
JSSS-Find.exe -u https://example.com -vue
```
上述命令会从 `https://example.com` 提取JS文件、进行vue测试

```bash
JSSS-Find.exe -u https://example.com -v
```
上述命令会从 `https://example.com` 提取JS文件、进行漏洞测试

```bash
JSSS-Find-AI.exe -ai -clean -url https://example.com/ JS的具体路径
```
上述命令会从指定文件夹中分析JS

```bash
JSSS-Find-AI.exe -ai -fuzz -clean -url https://example.com/ JS的具体路径
```
上述命令会从指定文件夹中分析JS，并根据 `https://example.com` 构造请求

# 内测体验方式：
![](https://github.com/kk12-30/JSSS-Find/blob/main/fenchuan.png)
