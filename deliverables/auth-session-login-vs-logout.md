# Auth Session Analysis: Login vs Logout (DVWA)

## Summary
本报告验证：DVWA 登录会建立有效会话（后续请求携带会话 Cookie 后可访问受限模块），注销会使会话失效（注销后再访问同一模块会回到登录态）。结论基于 Req/Res 成对证据。

## Evidence (Req/Res)
- A1 Login Request (Burp): [W1D1-Login-Req-Low.png]<img width="1718" height="908" alt="554791291-5c2b2ed8-b2f2-49f4-b9af-ca13c5553a3e" src="https://github.com/user-attachments/assets/720b463f-3714-4204-9fa4-cacb1b5925da" />

- A2 Login Result (Browser): [W1D1-Login-Res-Low.png]<img width="1718" height="908" alt="554791397-d6de3d3c-b003-4855-abe7-1cc19beb83aa" src="https://github.com/user-attachments/assets/4fc26fe1-c7d0-4b0f-b9cf-88a40705b1ab" />

- A3 Logout Request (Burp): [W1D2-Logout-Req.png]<img width="1718" height="908" alt="555245927-27e44433-59d2-40f9-a84d-abaf5e269941" src="https://github.com/user-attachments/assets/6dbbc845-3339-424f-98ef-fb96a58a8b73" />

- A4 Logout Result (Browser): [W1D2-Logout-Res.png]<img width="1718" height="908" alt="555245937-7be67328-bb7d-414d-9d04-30729839199b" src="https://github.com/user-attachments/assets/6c932f40-68c6-4dc4-8f8b-f783fd63525c" />

## Conclusion
登录与注销的核心差异是“会话/登录态是否有效”。登录时客户端向登录接口提交用户名/密码参数（见 A1），服务端建立会话并使浏览器进入 DVWA 主界面（见 A2）。此后客户端在后续请求中携带会话标识（Cookie/Session），访问功能模块不再被要求登录。注销时客户端访问注销接口（见 A3），服务端使当前会话失效（可能表现为会话在服务端被销毁、或 Cookie 过期/被清空），浏览器回到未登录态/登录页（见 A4）。若补充“注销后访问同一模块会跳回登录态”的证据，将形成完整复现闭环。

## Reproduce
1. 登录（A1→A2）
2. 访问任意模块页面（应不再要求登录）
3. 注销（A3→A4）
4. 再次访问同一模块（应跳回登录态；建议补图）
