# Web 应用安全测试与标准化交付（DVWA Lab）

> 60s 验收：本仓库为企业级单站点渗透测试实战成果，包含 2 篇标准化交付报告（登录/会话 与 HTTP 流量篡改），累计保留 5 组 Req/Res 证据对，适合作为简历项目展示与面试讲解素材。

## Quick facts
- Target: DVWA 靶场（local）
- Deliverables: 2 × standardized reports (`deliverables/`)
- Evidence: 5 × Req/Res pairs in `notes/`
- Test tools: Burp Suite (Proxy / Repeater / Intruder), sqlmap, Python scripts

## 目录（快速跳转）
- `deliverables/`  
  - `session-report.md` — 登录 / 会话安全分析  
  - `tamper-report.md`  — HTTP 流量篡改 / 会话复用测试
- `notes/` — 证据层（仅保留可复现 Req/Res 对）
- `assets/` — 流程图与截图

## 60s 验收步骤（面试用）
1. 打开 `deliverables/session-report.md`，看摘要与风险评分。  
2. 打开 `notes/session-evidence.md`，确认至少 1 对 Req/Res 截图与报告匹配。  
3. 打开 `deliverables/tamper-report.md`，看复现步骤与复测标准。

## 合法性声明
本项目仅用于授权测试与学习演练，禁止将本仓库内容用于未授权的攻击或扫描。
