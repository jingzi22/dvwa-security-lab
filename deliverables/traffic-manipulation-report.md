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
  <img width="659" height="914" alt="555275272-81d71bb2-f2c2-4f90-98bc-4dce996c327b" src="https://github.com/user-attachments/assets/c9fc180e-e3e6-491d-b214-b4eeed5916de" />


- **T2 - 服务端响应 (Response)**:
  > 服务端返回 `200 OK`，正常响应页面内容，证明未对非标准 UA 进行拦截或过滤。
  <img width="902" height="786" alt="555275304-74e81a8f-397b-4905-b753-07e49a3f16be" src="https://github.com/user-attachments/assets/4cef6ed2-b444-45be-b4b2-fdadfc062e68" />

### 2. 安全等级逻辑绕过 (Cookie Manipulation)
**测试目标**：验证是否可以通过修改 Cookie 强制变更系统的安全等级。

- **T3 - 低安全等级指纹 (Low Level)**:
  > 抓包显示当前 Cookie 为 `security=low`。此时系统不过滤任何输入。
  <img width="1718" height="908" alt="554791291-5c2b2ed8-b2f2-49f4-b9af-ca13c5553a3e" src="https://github.com/user-attachments/assets/c83458f1-954a-4b7b-8c8c-07c5a4aae770" />

- **T4 - 安全等级 Cookie 验证 (Cookie Analysis)**:
  > 通过 Web 界面切换安全等级至 Medium，抓取后续请求发现 Cookie 中的 `security` 参数值已同步变为 `medium`。
  > **分析结论**：证实系统通过客户端 Cookie (`security=low/medium/high`) 来标记当前会话的安全防御等级。
  <img width="1718" height="908" alt="555791603-4d426fd6-1655-4519-975b-02e702139f60" src="https://github.com/user-attachments/assets/74430399-0af0-4ce0-9a3e-0c9c3a1146db" />

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
