## 今日目标
总结 DVWA “登录 vs 注销”差异，形成可验收结论（200–300 字），并绑定证据文件名。

## 证据引用（【留痕】）
 登录请求：`W1D1-Login-Req.png`
<img width="1718" height="908" alt="W1D1-Login-Req-Low" src="https://github.com/user-attachments/assets/8c855dd2-896f-4ddd-af1e-8fa8e2f50126" />

 登录后主界面：`W1D1-Login-Res.png`<img width="1718" height="908" alt="W1D1-Login-Res-Home" src="https://github.com/user-attachments/assets/32cbbc8f-aea4-4b3e-8abf-cb2f51697cc0" />

 注销请求：`W1D2-Logout-Req.png`<img width="1718" height="908" alt="555245927-27e44433-59d2-40f9-a84d-abaf5e269941" src="https://github.com/user-attachments/assets/e1938dfb-bf2e-4385-aa47-12f772b8904b" />

 注销后未登录态页面：`W1D2-Logout-Res.png`<img width="1718" height="908" alt="555245937-7be67328-bb7d-414d-9d04-30729839199b" src="https://github.com/user-attachments/assets/40d3d47c-9ffa-4ec7-9fe0-6b534a1786e3" />

## 结论（200–300字）
登录与注销的本质差异是“会话/登录态是否有效”。
登录时客户端向登录接口提交账号密码参数（见 `W1D1-Login-Req.png`），
服务端在响应中下发/更新会话标识（如 `Set-Cookie` 或会话 Cookie 变化），
浏览器后续请求携带该 Cookie 后即可进入 DVWA 主界面并访问各功能模块（见 `W1D1-Login-Res.png`）。
注销时客户端访问注销接口（见 `W1D2-Logout-Req.png`），
服务端使当前会话失效（例如 Cookie 过期/被清空/会话在服务端被销毁），
因此页面回到登录态或提示未登录（见 `W1D2-Logout-Res.png`）。

## 可复现验证
 登录后直接打开任意模块页面不再要求登录。
