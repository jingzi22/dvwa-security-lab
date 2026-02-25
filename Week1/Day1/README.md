# Week1 - Day1

## 目标 (Objective)
完成 DVWA 数据库初始化，并验证登录请求与响应流程。

## 操作步骤 (Steps)
1. 访问 /dvwa/setup.php
2. 点击 Create / Reset Database
3. 使用 admin / password 登录
4. 使用 Burp 抓取 POST /dvwa/login.php
5. 验证成功跳转至 index.php

## 证据 (Evidence)
- W1D1-DBReset-Success.png
- W1D1-Login-Req-Low.png
- W1D1-Login-Res-Home.png

## 关键发现 (Key Findings)
- 登录使用 POST 请求
- 参数包含 username、password、user_token
- Cookie 中包含 security=low
- 返回 302 重定向到 index.php

## 待研究问题 (Questions)
- 302 重定向机制是什么？
- user_token 如何生成？
- security=low 是否由 Cookie 控制？
