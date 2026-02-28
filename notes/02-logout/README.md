## 目标 (Objective)
完成 Burp 代理配置，捕获注销（Logout）请求并验证注销后的页面状态。

## 操作步骤 (Steps)
1. 配置浏览器代理指向 Burp Suite（默认 127.0.0.1:8080）
2. 登录 DVWA 系统（admin/password）
3. 开启 Burp 拦截功能
4. 点击页面 Logout 按钮，捕获注销请求
5. 关闭拦截，验证页面跳转至登录页/未登录提示

## 证据 (Evidence)
- W1D2-Logout-Req.png <img width="1718" height="908" alt="W1D2-Logout-Req" src="https://github.com/user-attachments/assets/27e44433-59d2-40f9-a84d-abaf5e269941" />

- W1D2-Logout-Res.png <img width="1718" height="908" alt="W1D2-Logout-Res" src="https://github.com/user-attachments/assets/7be67328-bb7d-414d-9d04-30729839199b" />


## 关键发现 (Key Findings)
- 注销请求多为 GET/POST 方式（视 DVWA 版本而定）
- 注销后 Cookie 中的登录态失效
- 响应状态码多为 200/302，页面跳转至登录页

## 待研究问题 (Questions)
- 注销操作是否清除服务端 Session？
- 不同 security 级别下注销逻辑是否有差异？
- Logout 请求是否存在 CSRF 防护机制？
