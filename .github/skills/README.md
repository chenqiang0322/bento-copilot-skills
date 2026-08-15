# Bento Skills（GitHub Copilot Agent Skills）

本目录包含 3 套可直接提交到任意 GitHub 仓库的 **Agent Skill**，遵循 [agentskills.io](https://agentskills.io) 规范，会被 GitHub Copilot（云端 agent / 代码审查 / CLI / VS Code agent 模式）自动发现并加载。

## 目录结构

```
.github/skills/
├── bento-ui/        # Bento 设计系统 guideline（教 AI 生成 bento box 栅格界面）
│   └── SKILL.md
├── bento-cli/       # Bento 邮件营销 CLI 使用指南（安全批量操作）
│   └── SKILL.md
├── bento-ppt/       # Bento 网格风格 PPT/HTML deck 生成器（含模板与 4 个参考文件）
│   ├── SKILL.md
│   ├── assets/
│   │   └── template.html   # 完整可运行种子（含 3 个示例 slide）
│   └── references/
│       ├── themes.md       # 5 套主题色（只能选不能改）
│       ├── layouts.md      # 13 种 bento 布局骨架
│       ├── components.md   # 组件手册
│       └── checklist.md    # P0–P3 质量清单
└── README.md
```

## 三套 skill 说明

| 目录 | 触发场景 | 来源上游 |
|---|---|---|
| `bento-ui` | 让 AI 产出 bento box 卡片栅格 UI / 设计系统规范 | bergside/awesome-design-skills |
| `bento-cli` | 用 bentonow Bento CLI 做订阅者 / 标签 / 事件 / 广播的安全批量运维 | bentonow/bento-cli |
| `bento-ppt` | 生成 Apple keynote 风的单文件 HTML 网页 PPT（bento 网格） | by4hp/bento-ppt-skill |

## 部署到 GitHub 仓库

1. 把整个 `.github/` 目录复制（或合并）到**目标仓库根目录**：
   ```bash
   cp -r .github /path/to/your-repo/
   cd /path/to/your-repo
   git add .github
   git commit -m "chore: add bento skills for GitHub Copilot"
   git push
   ```
2. 提交后，仓库内的 Copilot agent 会自动索引这三套 skill。
3. 在 Copilot Chat 中用 `/` 即可看到 `bento-ui` / `bento-cli` / `bento-ppt`，或直接用自然语言触发（如「用 bento 风格给我做个产品发布会 PPT」）。

## 命名约定（agentskills.io 强制）

- 每个 skill 一个独立目录，目录名 = SKILL.md 中 `name` 字段（小写 + 连字符）。
- 本目录已统一为：`bento-ui` / `bento-cli` / `bento-ppt`。

## 注意事项

- `bento-ppt` 的 `template.html` 通过本地 `assets/motion.min.js` + CDN 双保险加载动效。
  本地未附带 `motion.min.js` 时，会自动回退到 jsDelivr CDN（需联网）；如需完全离线，
  可从上游仓库拷贝 `assets/motion.min.js` 到同目录。
- `bento-ui` / `bento-cli` / `bento-ppt` 的 SKILL.md 均已声明 `upstream` 元数据，便于溯源与更新。
