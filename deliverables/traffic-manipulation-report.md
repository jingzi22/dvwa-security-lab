# Traffic Manipulation Audit: HTTP Headers & Cookies

## Summary (审计摘要)
本次审计验证了 DVWA 目标系统在 HTTP 请求头处理与访问控制逻辑上的安全缺陷。
测试确认服务端对客户端提交的 `User-Agent` 头部缺乏有效校验，且系统的安全防御等级（Security Level）完全依赖客户端 Cookie 参数 `security` 控制。攻击者可通过篡改这些本地参数，绕过服务端的逻辑判断或强制降低系统的安全防御能力。

---

## Evidence (审计证据)

### 1. User-Agent 伪造 (Header Manipulation)
**测试目标**：验证服务端是否信任客户端自定义的 User-Agent 头部。

- **T1 - UA 篡改请求 (Request)**:
  > 在 Repeater 中将 User-Agent 修改为 `Hello-Hacker` 并发送。
  
  ![UA Modified Request](../notes/02_Traffic_Manipulation/W1D3-UA-Modified-Repeater.png)

- **T2 - 服务端响应 (Response)**:
  > 服务端返回 `200 OK`，正常响应页面内容，证明未对非标准 UA 进行拦截或过滤。
  
  ![UA Server Response](../notes/02_Traffic_Manipulation/W1D3-UA-Response.png)

### 2. 安全等级逻辑绕过 (Cookie Manipulation)
**测试目标**：验证是否可以通过修改 Cookie 强制变更系统的安全等级。

- **T3 - 低安全等级指纹 (Low Level)**:
  > 抓包显示当前 Cookie 为 `security=low`。此时系统不过滤任何输入。
  
  ![Cookie Security Low](../notes/02_Traffic_Manipulation/W1D4-Cookie-Low.png)

- **T4 - 等级参数篡改 (Medium Level)**:
  > 直接在请求包中将 Cookie 修改为 `security=medium`。系统逻辑随即切换至中级防御模式（如增加 `mysqli_real_escape_string`），证明安全逻辑由客户端参数直接驱动，存在逻辑漏洞。
  
  ![Cookie Security Medium](../notes/02_Traffic_Manipulation/W1D4-Cookie-Medium.png)

---

## Conclusion (技术结论)
系统存在 **"Insecure Design" (不安全设计)** 与 **"Trust Boundary Violation" (信任边界违规)** 问题。

1.  **校验缺失**：服务端无条件信任 HTTP 请求头，这使得攻击者可以伪装成爬虫（如 GoogleBot）或正常浏览器绕过初级 WAF 规则，也便于自动化扫描工具隐藏特征。
2.  **逻辑缺陷**：将核心的安全配置（Security Level）下放至客户端 Cookie 存储。攻击者无论当前在数据库中的配置如何，均可利用 Burp Suite 拦截流量并强制将 `security` 参数重置为 `low`，从而在攻击过程中始终面对最脆弱的防御逻辑。

---

## Reproduce (复现步骤)
1.  **环境准备**：启动 Burp Suite 并开启拦截模式。
2.  **UA 测试**：
    *   访问 DVWA 任意页面，拦截请求。
    *   发送至 Repeater，将 `User-Agent` 值改为任意字符串。
    *   点击 Send，观察 Response 状态码为 200。
3.  **Cookie 测试**：
    *   观察当前 Cookie 中的 `security` 值。
    *   手动修改该值为 `low` 或 `medium`，发送请求。
    *   观察响应内容或页面表现的变化（如 SQL 注入报错样式的改变），确认等级切换生效。
