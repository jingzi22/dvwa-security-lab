# Week1 - Day4

## 目标 (Objective)
完成 DVWA 安全等级从 Low 切换到 Medium，并验证 Cookie 中的 security 字段是否同步生效。

## 操作步骤 (Steps)
1. 登录 DVWA 系统（admin/password），点击顶部导航进入 DVWA Security 页面
2. 在安全级别下拉菜单中，将 Low 切换为 Medium
3. 点击 Submit 按钮提交设置，确认页面提示切换成功
4. 开启 Burp 代理，访问 DVWA 任意页面（如 security.php）
5. 在 Burp Proxy 中查看捕获的请求，定位 Cookie 头部进行对比

## 证据 (Evidence)
- W1D4-Security-Medium.png
<img width="1718" height="908" alt="W1D4-Security-Medium" src="https://github.com/user-attachments/assets/00666f28-8ac5-4466-a29d-a52594039878" />

- W1D4-Cookie-Security-Compare.png
<img width="1718" height="908" alt="W1D4-Cookie-Security-Compare" src="https://github.com/user-attachments/assets/4d426fd6-1655-4519-975b-02e702139f60" />

## 关键发现 (Key Findings)
- 安全级别切换成功后，页面会显示 “Security level set to Medium”
- Cookie 中的核心标识由 `security=low` 变更为 `security=medium`
- 该字段是服务端识别当前防护强度的关键依据，未切换将导致后续实验环境错误

## 待研究问题 (Questions)
- Medium 级别相比 Low 级别，在代码层面对输入增加了哪些过滤逻辑？
- 服务端是如何通过读取 Cookie 中的 security 值来加载不同防护策略的？
- 若手动修改 Cookie 为 `security=high`，是否能直接绕过页面设置提升等级？
