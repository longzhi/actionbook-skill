# actionbook-skill

ActionBook skill for OpenClaw: browser automation and web scraping with anti-detection stealth mode.

OpenClaw 的 ActionBook 技能：用于浏览器自动化与网页抓取，支持一定的反检测能力与动态页面处理。

---

## 中文简介

`actionbook-skill` 是一个面向 OpenClaw 的技能包，主要用于：

- 自动化网页操作（点击、输入、翻页、截图）
- 抓取 JavaScript 渲染后的页面内容
- 在 `web_fetch` 不够用时，改用浏览器级自动化完成任务
- 处理需要会话状态 / Cookie / 动态交互的网站

适用场景示例：

- 抽取某页面的结构化数据（标题、链接、时间、作者）
- 无登录状态下抓取公开信息流（如社交平台公开页）
- 进行可重复的网页工作流（检索 → 过滤 → 导出）

---

## English Overview

`actionbook-skill` is an OpenClaw skill package for browser automation and web scraping.

It is useful when you need to:

- Automate browser interactions (click, type, navigate, screenshot)
- Extract content from JavaScript-heavy pages
- Use browser-level workflows where `web_fetch` is not sufficient
- Work with session/cookie-based browsing flows

Typical use cases:

- Collect structured fields (title, URL, date, author) from web pages
- Scrape public timeline/feed pages without manual browsing
- Run repeatable web tasks (search → filter → export)

---

## 用法 / Usage

### 1) 在 OpenClaw 中调用技能

在聊天里直接描述任务，例如：

- `用 actionbook 抓取这个页面前 20 条标题和链接：<URL>`
- `用 actionbook 打开页面并截图，保存到 workspace`
- `用 actionbook 进入列表页，翻 3 页，导出所有项目链接`

You can ask naturally in chat, for example:

- `Use actionbook to extract the first 20 titles and links from <URL>.`
- `Use actionbook to open this page and save a screenshot.`
- `Use actionbook to paginate 3 pages and export all item links.`

### 2) 目录结构

- `SKILL.md`：技能说明与执行规范
- `scripts/fetch_tweet.sh`：示例抓取脚本
- `references/commands.md`：常用命令说明
- `references/selectors.md`：选择器与页面定位参考

### 3) 开发与维护

```bash
# 克隆仓库
git clone https://github.com/longzhi/actionbook-skill.git
cd actionbook-skill

# 本地修改后提交
git add .
git commit -m "docs: update README"
git push
```

---

## 注意事项 / Notes

- 请仅抓取你有权限访问或法律允许的数据。  
- 避免对目标站点发起高频请求，遵守 robots 与服务条款。  
- 对易变页面，优先使用稳定选择器并加入重试/超时控制。  

Please scrape responsibly and comply with target site policies and applicable laws.

---

## Repository

- GitHub: https://github.com/longzhi/actionbook-skill
