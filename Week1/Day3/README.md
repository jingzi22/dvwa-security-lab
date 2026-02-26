Week1 - Day3
目标 (Objective)
掌握 Burp Repeater 重放功能，修改 HTTP 请求头中的 User-Agent 字段并验证请求有效性。
操作步骤 (Steps)
登录 DVWA 系统（admin/password），刷新首页捕获已登录状态的 GET /dvwa/index.php 请求右键该请求，选择 Send to Repeater 发送至重放模块在 Repeater 左侧 Request 区域，找到 User-Agent 行并修改为 User-Agent: Hello-Hacker点击 Repeater 左上角 Send 按钮发送修改后请求查看右侧 Response 区域，验证响应状态码与页面内容是否正常
证据 (Evidence)
W1D3-Repeater-UA-Modify.png
W1D3-Repeater-Response-Success.png
关键发现 (Key Findings)
修改 User-Agent 字段不影响已登录请求的有效性服务器返回 200 OK 状态码，证明自定义 User-Agent 可正常被服务端接收User-Agent 字段无服务端校验，支持任意自定义内容修改
待研究问题 (Questions)
User-Agent 字段的实际业务用途有哪些？不同网站对 User-Agent 的校验规则是否存在差异？修改 User-Agent 能否绕过基础的风控 / 反爬机制？
