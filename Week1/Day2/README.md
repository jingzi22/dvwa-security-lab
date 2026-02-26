# Week1 Day2 任务记录

## Tue：Burp 代理跑通；抓「注销成功」

### 任务目标
- 确认 Burp 代理已正确配置并可正常拦截浏览器流量
- 捕获用户注销（Logout）操作的 HTTP 请求
- 验证注销后页面状态（回到登录页或提示未登录）

### 操作步骤
1. 配置浏览器代理，指向 Burp Suite 监听端口（默认 127.0.0.1:8080）
2. 登录 DVWA 系统
3. 开启 Burp 拦截，点击页面上的「Logout」按钮
4. 在 Burp 中查看并记录 Logout 请求详情
5. 关闭拦截，让请求发送到服务器，观察浏览器返回的页面状态

### 留痕

#### ① Logout 请求 Req 截图
<img width="1718" height="908" alt="0518b951e6a92cf5c0f550b8b341f967" src="https://github.com/user-attachments/assets/dbfa1053-f10f-4005-814d-b6bdc8e7b47c" />

#### ② 浏览器退出后页面 Res 截图
<img width="1718" height="908" alt="023560b382200fe74eb9db1cc6222508" src="https://github.com/user-attachments/assets/604264bd-d896-451b-a068-2b36ca225cb9" />
