# 跨平台兼容指南

本文档以 2026-07-23 可查到的官方能力为基线。仓库根目录的 `SKILL.md`、`references/` 和 `agents/openai.yaml` 是唯一知识源；平台包由 `scripts/build_compat.py` 生成到 `dist/`，不提交生成物，也不让适配说明进入技能运行上下文。

## 兼容矩阵

| 平台 | 兼容级别 | 使用形态 |
|---|---|---|
| Codex / ChatGPT 桌面端 | 原生 | 直接读取 Agent Skill；也可生成 Plugin 用于安装和分享 |
| ChatGPT Work 网页端 | 原生分发 | 通过生成的 OpenAI Plugin 分享到工作区 |
| TRAE Work / SOLO / IDE | 原生打包 | 上传带目录包裹的 ZIP，或复制到 TRAE 技能目录 |
| Hermes Agent | 原生 | 将仓库放入 Hermes 技能目录，直接读取 `SKILL.md` 与引用文件 |
| OpenClaw | 原生 | 从 Git 仓库或本地目录安装 Agent Skill |
| 扣子 / Coze | 转换兼容 | 系统提示词 + 知识库；插件和工作流只承担外部动作 |

## 一次生成全部适配产物

在仓库根目录运行：

```powershell
python .\scripts\build_compat.py
```

也可以只生成某一类：

```powershell
python .\scripts\build_compat.py --platform trae
python .\scripts\build_compat.py --platform openai
python .\scripts\build_compat.py --platform coze
python .\scripts\build_compat.py --platform portable
```

脚本在生成前会检查技能名称与本地引用链接。`dist/` 已被 Git 忽略，可随时重建。

## Codex 与 ChatGPT

### 个人技能

当前 Codex 与 ChatGPT 桌面端使用开放 Agent Skills 结构，可将仓库克隆到个人技能目录：

```powershell
git clone https://github.com/qlhouseClub/product-expert.git "$env:USERPROFILE\.agents\skills\product-expert"
```

### ChatGPT Work / 团队分发

生成 OpenAI Plugin 与本地 Marketplace：

```powershell
python .\scripts\build_compat.py --platform openai
codex plugin marketplace add .\dist\openai-marketplace
```

重启 ChatGPT 桌面端，在 Plugins 中安装“产品专家”。需要团队使用时，可从插件详情页分享到 ChatGPT 工作区。生成的单插件压缩包位于 `dist/openai/product-expert-plugin.zip`。

## TRAE Work / SOLO / IDE

生成上传包：

```powershell
python .\scripts\build_compat.py --platform trae
```

在 TRAE 的“设置 → 技能与命令/规则和技能 → 创建或上传技能”中选择 `dist/trae/product-expert.zip`。压缩包采用 `product-expert/SKILL.md` 的目录包裹结构。

项目级安装可将完整技能目录复制到：

```text
<项目>/.trae/skills/product-expert/
```

Windows 全局技能目录通常为：

```text
%USERPROFILE%/.trae-cn/skills/product-expert/
```

部分 TRAE 版本曾出现 ZIP 导入后只保留 `SKILL.md`、丢失 `references/` 的问题。导入后应检查引用文件是否完整；若缺失，改用完整文件夹复制方式。

## Hermes Agent

Hermes 原生识别 `SKILL.md`、`references/`、`scripts/`、`assets/` 等结构。可将仓库直接放入个人技能目录：

```powershell
git clone https://github.com/qlhouseClub/product-expert.git "$env:USERPROFILE\.hermes\skills\product-expert"
```

也可以生成 `dist/portable/product-expert.zip`，解压到 `~/.hermes/skills/`。仓库是私有仓库时，在线安装需要有效的 GitHub 凭据或 Token。

## OpenClaw

OpenClaw 可从 Git 仓库安装根目录包含 `SKILL.md` 的技能：

```text
openclaw skills install git:qlhouseClub/product-expert@main
```

也可以在本地仓库目录执行：

```powershell
openclaw skills install 'E:\product-expert' --as product-expert
```

默认安装到当前工作区的 `skills/`；需要所有本地 Agent 共享时使用 `--global`。私有 Git 仓库同样需要可用的 GitHub 凭据。

## 扣子 / Coze

扣子当前以智能体提示词、知识库、插件和工作流为核心，并不原生读取 Agent Skills 目录。生成转换包：

```powershell
python .\scripts\build_compat.py --platform coze
```

然后：

1. 将 `dist/coze/product-expert/agent-prompt.md` 粘贴到智能体系统提示词。
2. 新建知识库，上传 `dist/coze/product-expert/knowledge/` 中全部 Markdown 文件。
3. 把知识库绑定到智能体并启用检索。
4. 只有需要联网、数据库或外部写操作时，再配置扣子插件或工作流。
5. 用真实业务任务验证检索命中、证据标注、工作深度和输出稳定性。

扣子层是“行为桥接 + RAG”，不是把 `SKILL.md` 假装成扣子的原生插件。知识仍由根目录文件维护，重新运行脚本即可同步。

## 维护规则

1. 专业能力只修改 `SKILL.md` 与 `references/`。
2. OpenAI 界面元数据只修改 `agents/openai.yaml`。
3. 扣子的最小行为桥接只修改 `platforms/coze/agent-prompt.md`。
4. 平台名称、仓库、展示文案与版本只修改 `platforms/manifest.json`。
5. 不手工编辑 `dist/`；任何平台包都应重新生成。

## 官方依据

- [OpenAI Build skills](https://learn.chatgpt.com/docs/build-skills)
- [OpenAI Build plugins](https://learn.chatgpt.com/docs/build-plugins)
- [TRAE 官方中文社区：技能目录与导入](https://forum.trae.cn/t/topic/31835)
- [TRAE 官方中文社区：ZIP 目录结构](https://forum.trae.cn/t/topic/17685)
- [Hermes Agent Skills](https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/skills.md)
- [OpenClaw Skills](https://github.com/openclaw/openclaw/blob/main/docs/tools/skills.md)
- [Coze Studio 功能清单](https://github.com/coze-dev/coze-studio)
- [Coze Studio 插件配置](https://github.com/coze-dev/coze-studio/wiki/4.-%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE)
