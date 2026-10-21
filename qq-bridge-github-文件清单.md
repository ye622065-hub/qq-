# qq-bridge 发布文件集说明

生成时间：2026-10-21
源目录：`D:\deepseek111\qq.bridge`
发布目录：`D:\deepseek111\qq-bridge-github`
压缩包：`D:\deepseek111\qq-bridge-github.zip`

---

## 一、这套文件是什么

用于上传 GitHub 的干净副本，共 **138 个文件 / 2.58 MB**，目录结构与原项目一致：

| 目录/文件 | 内容 |
|---|---|
| `src/` | 桥接主程序、DSH 客户端、MCP server、语音/表情/黑话等模块（24 个文件） |
| `scripts/` | 安装、验证、测试与运维脚本（77 个文件） |
| `dsh/` | `qq-chat` / `qq-chat-v2` 两套 agent preset 源文件 |
| `plugins/` | `qq-agent-presets`、`qq-mode-console` 两个 DSH bundle |
| `roles/` | 角色卡（`小鲸鱼.md`、`傲娇助手.md`）与说明 |
| `docs/` | 公开文档（安装、隐私、安全基线、控制台等 7 个文件） |
| `assets/` `public/` | 项目图片与控制台静态页 |
| 根目录 | `README.md` / `README.en.md` / `LICENSE` / `RULES.md` / `package.json` / `package-lock.json` / `config.example.json` / `start*.bat` / `restart.bat` / `.gitignore` / `.npmrc` |

---

## 二、刻意排除的内容（不要上传）

| 排除项 | 原因 |
|---|---|
| `config.json` | 含真实 SnowLuma accessToken、consoleToken、QQ 号与白名单 |
| `state/` | 运行时状态：聊天记录、会话映射、控制台令牌、表情/黑话/记忆数据 |
| `node_modules/` | 依赖，由 `npm install` 生成 |
| `_meta/` | 恢复过程证据（会话回放、补丁清单） |
| `_recovered_winfr/` | winfr 恢复出的乱码碎片，无使用价值 |
| 根目录 `_*.mjs`、`_snowluma-catalog.json` | 本机一次性调试脚本/抓取数据 |
| `README-恢复说明.md`、`安装说明.md` | 含本机路径、恢复过程与初始密码等私人信息 |
| `scripts/privacy-rules.json`、`audio/` | 本机隐私规则与个人音频素材 |
| `*.log`、`*.bak*` | 运行日志与备份 |

> 以上排除项在 `.gitignore` 中已有对应规则，后续 `git add` 不会误带。

---

## 三、安全核查

已对发布目录做全文扫描，以下内容均为 **0 命中**：

- 真实 token（SnowLuma HTTP/WS、控制台、旧版 token）
- 真实 QQ 号（机器人、owner、群号、好友号）
- 本机路径（`D:\deepseek111`、`C:\Users\...`、`D:\SnowLuma`）
- 用户名、控制台初始密码

`config.example.json` 是脱敏模板，可直接公开。

---

## 四、上传 GitHub 的步骤

本机没有安装 git，可在任意装有 Git 的机器上执行（或先安装 Git for Windows）：

```bash
cd D:\deepseek111\qq-bridge-github
git init
git add .
git commit -m "qq-bridge: DSH 0.2.x 适配版"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

如果仓库已存在，先 `git pull --rebase origin main` 再推送。

---

## 五、版权与来源说明

- 本项目上游为 **Derpyu520/qq-bridge**（MIT），本副本是在其 v0.2.0 基础上恢复并做本地适配的版本，`LICENSE` 与 README 中的上游链接均已保留；
- 公开发布时请保留 MIT 许可证与上游署名；
- 本副本相对上游的本地改动包括：`qq-chat` / `qq-chat-v2` 预设的 `{{cwd}}` 变量修复（DSH 0.2.1 不再注册该变量）、按 0.2.1-rc.2 调整的 MCP 挂载路径等。

---

## 六、注意

- 发布目录里没有 `config.json`，别人克隆后需按 README 复制 `config.example.json` 并填自己的 QQ/OneBot 信息；这是刻意的 fail-closed 设计。
- `docs/` 只保留了公开文档；原 `.gitignore` 中列出的 `docs/audits/`、`docs/design/`、`docs/research/`、`docs/legacy/` 等内部文档未包含。
