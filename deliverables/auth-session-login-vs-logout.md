# Auth Session Analysis: Login vs Logout (DVWA)

## Summary
本报告验证：DVWA 登录会建立有效会话（后续请求携带会话 Cookie 后可访问受限模块），注销会使会话失效（注销后再访问同一模块会回到登录态）。结论基于 Req/Res 成对证据与“注销后再访问受限模块”的验证证据。

---

## Evidence (Req/Res)

### Login
- A1 Login Request (Burp)
<img width="1718" height="908" alt="554791291-5c2b2ed8-b2f2-49f4-b9af-ca13c5553a3e" src="https://github.com/user-attachments/assets/c10c0acc-da65-4cfc-a2a9-1b931facbeb0" />

- A2 Login Result (Browser)
<img width="1718" height="908" alt="554791397-d6de3d3c-b003-4855-abe7-1cc19beb83aa" src="https://github.com/user-attachments/assets/8c71ac34-3fe5-4bf4-aeb7-98fb420fb7a4" />

### Logout
- A3 Logout Request (Burp)
<img width="1718" height="908" alt="555245927-27e44433-59d2-40f9-a84d-abaf5e269941" src="https://github.com/user-attachments/assets/f6ac741e-1833-4a27-8340-6319ab057c85" />

- A4 Logout Result (Browser)
<img width="1718" height="908" alt="ad2e612d-7314-47df-bece-d1353cc133fc" src="https://github.com/user-attachments/assets/21a3ed1f-7850-4009-8b8b-a1a332c15d8e" />


### Post-Logout Verification (Required)
- A5 After logout, access protected module again (e.g., security.php) -> back to login state:
  - - [W1D2-After-Logout-Access-Denied.png](https://github.com/user-attachments/assets/11c64ac6-9655-4150-81cf-98bd60c11d5a)


---

## Conclusion (200–300字)
登录与注销的核心差异是“会话/登录态是否有效”。登录时客户端向登录接口提交用户名/密码参数（见 A1），服务端建立会话并使浏览器进入 DVWA 主界面（见 A2）。此后客户端在后续请求中携带会话标识（Cookie/Session），访问受限功能模块不再被要求登录。注销时客户端访问注销接口（见 A3），服务端使当前会话失效（可能表现为服务端 Session 销毁或客户端 Cookie 登录态失效），浏览器回到未登录态/登录页（见 A4）。进一步验证显示：在不重新登录的情况下再次访问同一受限模块会被重定向回登录态（见 A5），说明注销后会话已失效，形成完整复现闭环。

---

## Reproduce (Checklist)
1. 登录 DVWA，抓包保存登录 Req/Res（A1 → A2）
2. 访问任意受限模块页面（例如 `security.php`），确认可访问
3. 点击 Logout，抓包保存注销 Req/Res（A3 → A4）
4. 再次访问 `security.php`，应跳回登录态/登录页（A5）
