适用于 LeviTK 工作流的 Agent Skills 仓库。

本仓库遵循 [Agent Skills 规范](https://agentskills.io/specification)。其中的技能面向支持 `SKILL.md` 发现机制的代理工具，包括 Claude Code、Codex CLI、OpenCode，以及其他兼容的编码代理。

## 安装方式

### 通过 Marketplace 安装

```text
/plugin marketplace add LeviTK/LeviTK_Skills
/plugin install levitk-skills@LeviTK_Skills
```

### 通过 npx skills 安装

```bash
npx skills add git@github.com:LeviTK/LeviTK_Skills.git
```

### 手动安装

#### Claude Code

将仓库内容复制到项目根目录下的 `/.claude`。

#### Codex CLI

将 `skills/` 目录复制到 `~/.codex/skills`。

#### OpenCode

将完整仓库克隆到 OpenCode 的技能目录中：

```bash
git clone https://github.com/LeviTK/LeviTK_Skills.git ~/.opencode/skills/LeviTK_Skills
```

请克隆整个仓库，而不仅仅是内部的 `skills/` 目录，这样元数据和未来的共享资源才能一并保留。

## 技能列表

| 技能 | 说明 |
|-------|------|
| [heptabase-cli-cn](skills/heptabase-cli-cn) | 使用 Heptabase CLI 管理笔记、日记、标签、卡片、白板和 AI Tutor 内容的中文技能。 |
| [heptabase-mcp-cn](skills/heptabase-mcp-cn) | 使用 Heptabase MCP 工具搜索、读取、分析和写入 Heptabase 内容的中文技能。 |

## 仓库结构

```text
LeviTK_Skills/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── skills/
│   ├── heptabase-cli-cn/
│   │   └── SKILL.md
│   └── heptabase-mcp-cn/
│       ├── SKILL.md
│       └── references/
│           ├── Hep_Markdown.md
│           └── heptabase-mcp.md
├── LICENSE
└── README.md
```

每个技能都放在 `skills/<skill-name>/SKILL.md` 中。较大的参考资料应放在 `skills/<skill-name>/references/` 目录下，并从技能文件中进行链接。
