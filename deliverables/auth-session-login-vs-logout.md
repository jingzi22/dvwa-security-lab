# Auth Session Analysis: Login vs Logout (DVWA)

## Summary
本报告验证：DVWA 登录会建立有效会话（后续请求携带会话 Cookie 后可访问受限模块），注销会使会话失效（注销后再访问同一模块会回到登录态）。结论基于 Req/Res 成对证据。

## Evidence (Req/Res)
- A1 Login Request (Burp): [W1D1-Login-Req.png](../Week1/Day5/W1D1-Login-Req.png)
- A2 Login Result (Browser): [W1D1-Login-Res.png](../Week1/Day5/W1D1-Login-Res.png)
- A3 Logout Request (Burp): [W1D2-Logout-Req.png](../Week1/Day5/W1D2-Logout-Req.png)
- A4 Logout Result (Browser): [W1D2-Logout-Res.png](../Week1/Day5/W1D2-Logout-Res.png)

> 建议补充：注销后再次访问受限模块的结果图（AfterLogout Access），让验证闭环更完整。

## Conclusion (200–300字)
登录与注销的核心差异是“会话/登录态是否有效”。登录时客户端向登录接口提交用户名/密码参数（见 A1），服务端建立会话并使浏览器进入 DVWA 主界面（见 A2）。此后客户端在后续请求中携带会话标识（Cookie/Session），访问功能模块不再被要求登录。注销时客户端访问注销接口（见 A3），服务端使当前会话失效（可能表现为会话在服务端被销毁、或 Cookie 过期/被清空），浏览器回到未登录态/登录页（见 A4）。若补充“注销后访问同一模块会跳回登录态”的证据，将形成完整复现闭环。

## Reproduce
1. 登录（A1→A2）
2. 访问任意模块页面（应不再要求登录）
3. 注销（A3→A4）
4. 再次访问同一模块（应跳回登录态；建议补图）
