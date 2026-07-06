# 通用 AI Agent 复盘系统

在一个对话中完成重要任务后，输入 `/复盘`，榨干整个对话的价值——把经验教训、决策、错误、好做法、可复用模式全部挖出来，沉淀为知识资产。

## 快速开始

1. 将 `.claude/commands/复盘.md` 复制到 `~/.claude/commands/`
2. 将 `.claude/skills/retro-*/` 复制到 `~/.claude/skills/`
3. 在 Claude Code 中输入 `/复盘`

## 架构

```
/复盘（轻薄命令入口）
    │
    ├─ 扫描对话 → 识别"值得注意的时刻"（错误/意外/决策/发现/恢复/效率）
    ├─ 判断领域 → 7 个领域（experiment/data/coding/research/debugging/design/其它）
    ├─ 每个领域 → 加载 retro-<domain> skill → 深度追问
    │   ├─ 有 skill → 按评估维度+反模式+正向模式+追问 深度分析
    │   └─ 没有 → 搜索行内经验 → 结构化 → 审查 → 确认 → 保存 → 复盘
    ├─ 对照已有知识 → 7 种关系判定（验证/补充/修正/升级/合并/矛盾/新建）
    ├─ 沉淀输出 → Rule/Lesson/Insight/Pattern/Action 按类型路由
    └─ 闭环验证 → 追踪产出是否被后续 Agent 使用
```

## 核心设计原则

- **质量优先**：skill 一次打磨，反复受益。复利。
- **平衡锚定**：同等重视问题识别和正向模式固化。
- **行内经验优先**：不从对话临时归纳，学习行内人踩过的坑。
- **入库 + 盘点并重**：不只写新文件，更维护存量知识。
- **闭环验证**：不止产出，更要追踪是否被使用。
- **渐进增长**：领域 skill 随使用积累，反模式和正向模式表随复盘自填充。

## 文件结构

```
.claude/
├── commands/
│   └── 复盘.md                    # /复盘 命令入口
└── skills/
    ├── retro-experiment/SKILL.md   # ML实验复盘
    ├── retro-data/SKILL.md         # 数据处理复盘
    ├── retro-coding/SKILL.md       # 代码复盘
    ├── retro-research/SKILL.md     # 调研复盘
    ├── retro-debugging/SKILL.md    # 调试复盘
    └── retro-design/SKILL.md       # 设计/架构复盘
docs/
├── design.md                       # 设计文档
└── adversarial-review-round*.md    # 审查记录
```

## 设计方法论

本系统的设计过程本身就是一个可复用的方法论：需求 → 广泛调研 → 第一性原理分析 → 多轮对抗性审查 → 用户对齐 → 最简实施。详见 `docs/design.md`。

---

🤖 由 Claude Code 辅助设计，以成品质量为最终目标。
