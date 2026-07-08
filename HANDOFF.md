# 复盘系统项目 — 会话恢复文档 (HANDOFF)

> **用途**：compact 后读此文档快速恢复工作状态。按 Anthropic long-running agent 最佳实践编写。
> **最后更新**：2026-07-08
> **当前会话目标**：复盘系统已完成核心实现，正处于"买 vs 造"决策点。

---

## 🎯 一句话状态

通用 AI Agent 复盘系统（`/复盘` 命令 + 6 个 retro-domain skill）已完整实现并推送 GitHub。调研发现 GitHub 上有 20+ 同类成熟项目，已 clone 3 个深度评测完毕。**下一步：决定"站在巨人肩上"的整合方案（混合方案 B 为主）。**

---

## 📍 Boot-up 检查清单（恢复后先做）

1. `pwd` 确认在 `D:/` 
2. 读本文档全文
3. 读 `D:/retrospective-system/docs/design.md`（设计文档 v7，系统最终形态）
4. 确认 GitHub 状态：`cd D:/retrospective-system && git log --oneline -5`（最新应含"三道防线"提交 5a1a213）
5. 读三个竞品评测（见下方"竞品评测结论"）
6. 向用户复述状态，等确认后再动手

⚠️ **网络陷阱**：本机 git push 在 Windows CMD 失败，但在 **Git Bash / 本 Agent 的 Bash 工具**中可成功。网络时断时续，push 失败就重试。

---

## 📦 已完成的资产

### 生效位置（~/.claude/，Claude Code 实际加载）
```
~/.claude/commands/复盘.md              # /复盘 命令（含三道防线）
~/.claude/skills/retro-experiment/SKILL.md
~/.claude/skills/retro-data/SKILL.md
~/.claude/skills/retro-coding/SKILL.md
~/.claude/skills/retro-research/SKILL.md
~/.claude/skills/retro-debugging/SKILL.md
~/.claude/skills/retro-design/SKILL.md
~/.claude/skills/adversarial-review/SKILL.md   # 全局对抗性审查
```

### 项目仓库（D:/retrospective-system/，GitHub 用）
```
D:/retrospective-system/
├── README.md, AGENTS.md, llms.txt      # GEO 优化文件
├── docs/design.md                       # 设计文档 v7（权威）
├── docs/adversarial-review-round[1-7].md
├── .claude/commands/复盘.md             # 命令副本
├── .claude/skills/retro-*/SKILL.md      # skill 副本
└── research/competitors/                # 3 个 clone 的竞品
    ├── claude-reflect/
    ├── learning-loop-skill/
    └── learned-behavior/
```
GitHub: `https://github.com/kaixin1seu/retrospective-system`（公开）

⚠️ **双份维护**：`~/.claude/` 生效，`D:/retrospective-system/.claude/` 是 Git 副本。改了生效版本要 `cp` 同步到项目版本再 commit。

---

## 🏆 竞品评测结论（关键决策依据）

| 项目 | 杀手锏 | 我们该借鉴的 |
|------|--------|-------------|
| **claude-reflect** (v2.6, 160测试) | hooks 自动捕获 + regex+语义双层检测 + `/reflect-skills` 模式发现 | SessionStart/UserPromptSubmit hooks 解决"手动触发"痛点 |
| **learning-loop** (v4.2, 极成熟) | scan/wrap-up 双模式 + 子代理隔离上下文 + watch-list 熟化成 plan + 量化 eval | 子代理隔离；它的 SKILL 充满和我们一样的"走捷径"坑，用 STOP gates 治，验证了我们三道防线方向对 |
| **learned-behavior** (有CI) | **零-LLM 纯 hook 行为信号挖掘走捷径** + fingerprint 聚类 + confidence 生命周期(candidate→approved→dormant→retired) | 它能自动检测我们手动发现的"Agent 走捷径"问题 |

### 我们真正独特的价值（不可放弃）
1. **7 种存量关系判定**（验证/补充/修正/升级/合并/矛盾/新建）— 别人多是简单 append
2. **平衡锚定**（正向模式表 + 检测信号）— 别人全是"失败→教训"单向
3. **领域透镜体系**（6 个 domain skill）— 别人全是通用复盘

### 我们的短板（需借鉴补齐）
1. 无 hooks 自动化（靠手动 `/复盘`）
2. 无 confidence + 生命周期机制
3. 无子代理隔离（复盘污染主上下文）

---

## ⏭️ 下一步（NEXT — 明确单一任务）

**决策点**：用户倾向"C 先评测 → 再执行 A 或 B"。评测（C）已完成。

**待用户确认的方向**：混合方案（B 为主，借鉴 A）
- 保留独特层（7种关系/平衡锚定/领域透镜）
- 借鉴 learned-behavior 的 hook 行为挖掘（自动检测走捷径）
- 借鉴 claude-reflect 的 SessionStart/UserPromptSubmit hooks（自动触发）
- README 诚实署名"站在巨人肩上"

**如果用户同意**：写正式的"对比报告 + 整合方案"文档，然后实施 hooks 层。

---

## 📋 待处理行动项（memory 中已记录）

优先级见各文件 frontmatter：
- `action_adversarial_review_upgrade.md` — 🔴 审查方法论升级（趋势驱动）
- `action_agent_self_correction_protocol.md` — 🔴 被批评时慌张协议
- `action_methodology_auto_trigger.md` — 🔴 方法论固化
- `action_criticism_response_skill.md` — 🔴 批评响应 skill
- `action_edit_precision_checklist.md` — 🟡 编辑精确性（含语言退化五模式）
- `action_new_session_reminder.md` — 新对话提醒（处理任务+推送 GitHub）
- `action_content_publishing.md` — 公众号/知乎发文（系统定型后）

---

## 🧠 本项目重要教训（已沉淀到 memory）

- `feedback_research_before_build.md` — **造轮子前先调研**（本项目最大教训）
- `reference_balanced_anchoring.md` — 评估框架需正负双向
- `feedback_product_quality_first.md` — 质量优先，不省 token
- `feedback_retro_execution_gaps.md` — Agent 走捷径的三种表现
- `reference_user_alignment_principle.md` — 审查发现需用户确认接受度

---

## ⚠️ 与本 Agent 协作的已知陷阱（burned before）

1. **走捷径**：Agent 倾向"对话变化不大→跳步骤"。/复盘 已加三道防线，但需警惕在其它任务中复发。
2. **修改时语言退化**："仅当""退回到"等不严谨词。改文档后自查语言精度。
3. **不调研就动手**：本项目反复出现。任何"做 X"先搜"GitHub 有没有 X"。
4. **被批评时慌张**：过度修正。应"暂停→溯源→再行动"。
5. **git push**：CMD 失败用 Bash 工具重试，非代理问题。
