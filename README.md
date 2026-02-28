# DVWA Security Lab (Evidence-driven)

本仓库记录基于 DVWA 的 Web 安全练习，按“真实交付”标准整理：每个主题包含 **复现步骤、Req/Res 证据链、结论与验证口径**。

---

## Start here (Deliverables)

- ✅ Auth Session Analysis (Login vs Logout)  
  - Report: `deliverables/auth-session-login-vs-logout.md`

> 如果只看最终成果：从 deliverables 进入即可。

---

## Quick Verification (60s)

1. 打开报告：`deliverables/auth-session-login-vs-logout.md`
2. 按报告里的 Evidence 链接查看 Req/Res 与截图证据
3. 按 Reproduce 步骤复现：登录建立会话、注销使会话失效

---

## Notes (Evidence & Process)

> notes 目录存放过程记录与证据材料（截图/要点/实验细节）。

- `notes/01-env-login/`：环境初始化 & 登录请求链路
- `notes/02-logout/`：注销请求链路 & 会话失效验证
- `notes/03-burp-repeater-ua/`：Burp Repeater / User-Agent 等基础操作记录
- `notes/04-security-level-medium/`：DVWA Security Level 调整与 Cookie/配置验证
- `notes/05-auth-session-analysis/`：登录 vs 注销的会话对比分析（支撑 deliverable）

---

## Conventions (Repo rules)

- 证据命名：`W<week>-<topic>-<Req|Res>-<desc>.png`（或保持你当前的命名体系，但要统一）
- 每个主题至少包含：
  - Steps（复现步骤）
  - Evidence（Req/Res + 截图）
  - Conclusion（200–300 字）
  - Reproduce（验证口径/检查点）
