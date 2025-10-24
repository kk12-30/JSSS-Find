# JSSS-Findv6.5: 自动化JS提取与测试工具 ![JSSS-Find Logo](https://img.shields.io/badge/Project-JSSS--Find-blue)


更新记录

```
v6.5: https://mp.weixin.qq.com/s/WqRqWhd8J4khAsKJldwZeg

v6.2: api_report.html报告中新增AI上下文理解功能，深度理解JavaScript代码片段，智能推断API参数和用法

V6.1:  修复前缀JS下载重试的bug

V6.0:  新增了「AI智能分析模式」,直接用AI分析复杂JS逻辑,自动构造出完整JS文件路径，告别手动拼接

V5.0:  https://mp.weixin.qq.com/s/AVyjVG0PZfZ5n-Ddv__q1g

V4.0： https://mp.weixin.qq.com/s/brZXggl989Kv3ywG_ZstxQ

```


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
JSSS-Find.exe -u <URL> [-fuzz] 
```

-  `-u <URL>`: 指定需要提取JS文件和进行测试的URL。
-  `-uf url.txt`:从文件中批量读取URL进行测试，每行一个URL，可在URL后空格添加BaseDir。
-  `-fuzz`: 启用fuzz测试。
-  `-m` 使用深度fuzz模式，构造大量请求参数进行fuzz（使用方式-fuzz -m）
-  `-api` 自动获取basedir（需存在路径文件C:\Program Files\Google\Chrome\Application\chrome.exe）
-  `-bypass` 会对401/403请求进行绕过测试
-  `-v`: 启用漏洞检测模式，速度较慢。
-  `-vueBrowser`: 在真实浏览器环境中访问Vue接口。

#### 读取本地JS文件目录 📂

```bash
JSSS-Find.exe -f <本地需要读取的JS目录> [-fuzz] [-v] [-vueBrowser]
```

- `-f <本地JS目录>`: 指定本地目录，工具会自动分析该目录下的所有JS文件。
- `可联动Packer-Fuzzer工具获取的js  该工具下载的js在tmp文件夹中`
- `读取小程序反编译后的JS，获取敏感信息和接口`


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


