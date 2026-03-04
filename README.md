# Web 应用安全测试与标准化交付（DVWA Lab）

> 60s 快速验收：本仓库为企业级单站点渗透测试实战成果，包含 3 个标准化漏洞报告（SQLi / XSS / Upload），共计 5 组 Req/Res 证据对，可作为简历项目展示与面试讲解素材。

## Quick facts
- Target: DVWA靶场（local）
- Deliverables: 3 × standardized reports (`deliverables/`)
- Evidence: 5 × Req/Res pairs in `notes/`  
- Test tools: Burp Suite (Proxy/Repeater/Intruder), sqlmap, Python scripts

## 目录（快速跳转）
- `deliverables/` — 对外标准化报告（可直接交付）
  - `sqli-report.md` | `xss-report.md` | `upload-report.md`
- `notes/` — 证据层（仅保留可复现 Req/Res 对）
  - `sqli-evidence.md` | `xss-evidence.md` | `upload-evidence.md`
- `assets/` — 流程图与截图

![Testing workflow](assets/flowchart.png)

> 本项目仅用于授权测试与学习，禁止未授权攻击。
