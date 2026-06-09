# 来源版本追踪（humanizer）

> 本文件按 skill-forge 规范记录 humanizer 的上游来源、本地定制史与上游同步状态。每次演进强制留痕。

## 上游来源

| 项 | 来源 | 说明 |
|----|------|------|
| 英文规则基底 | upstream: `blader/humanizer` | Wikipedia "Signs of AI writing" 的 skill 化 |
| ⚠️ 历史关系 | **不相关历史**（unrelated histories） | 当年是复制上游内容进全新 git，非 fork；`git merge-base master upstream/main` 为空 → **不能 cherry-pick**，上游更新只能手动移植 |
| 分支差异 | 本地 `master` / 上游 `main` | 比较用 `master..upstream/main` |

## 本地定制史

| 日期 | commit | 改动 | 来源 |
|------|--------|------|------|
| — | `c11eb93` | upstream baseline | blader/humanizer |
| 2026-04-09 | `6af8089` | sync to upstream latest（baseline = v2.5.1，规则 1-29） | blader/humanizer |
| 2026-05-04 | （chinese-ai-tells.md 创建） | `references/chinese-ai-tells.md`：10 条中文规则 + 张晨腔 vs AI 腔判别框架（4 判别问 + 三色标） | 梁樊导师 2026-05-04 反馈 10 条 + 仓库 `工具与环境/写作风格/` 6 篇笔记 |
| 2026-06-09 | `ab0effd` | chinese-ai-tells 新增规则 11 外交腔 + 规则 6/10 增强 + 示弱真伪边界 + 判别问 2 格言对举；SKILL.md description/Bilingual/Process 计数 10→11 | **qiu-zhijie-persona** skill 反外交病机制提取（会话 `9e4cb53e`） |

## 上游同步状态（2026-06-09 核查）

- **本地 baseline**：v2.5.1（英文规则 1-29）+ 中文模块（chinese-ai-tells 11 规则）
- **上游最新**：**v2.8.0**，领先本地 v2.6.0 / v2.7.0 / v2.8.0 + 若干 PR
- **上游新增、本地未合并**（手动移植候选）：

| 上游新增 | 版本 | 价值评估 | 与本地定制的关系 |
|---------|------|---------|-----------------|
| DETECTION GUIDANCE 段（What NOT to flag 误报防范 + Signs of human writing 保留） | v2.x | **高** | 与本地张晨腔判别框架、规则 10 正向、绿标放行**同源**，强化"不阉割"——优先移植 |
| 规则 32 Aphorism Formulas（格言公式视为 AI tell） | v2.x | 中 | ⚠️ **与本地 2026-06-09 新增"格言体对举合法"（判别框架）直接张力**——移植须加豁免：上游针对空洞人造格言，本地保护嵌入具体批评判断的格言对举 |
| 规则 31 Manufactured Punchlines and Staccato Drama | v2.x | 中 | 与推敲"短句突现"有张力，需判别 |
| 规则 33 Conversational Rhetorical Openers | v2.x | 中 | 通用，可移植（中文对应"让我来告诉你"式开场） |
| 规则 30 Diff-Anchored Writing | v2.7.0 | 低 | 针对 diff/PR 写作，中文学术场景价值低 |
| 规则 14 em/en dash 强化、规则 21 gap-filling 补充 | v2.7.0 | 低-中 | 小改进，可同步 |

- **移植记录（2026-06-09，会话 `9e4cb53e`，用户批准"全部 30-33 + 指引"）**：
  - ✅ 规则 30-33 + DETECTION GUIDANCE 已移植到 SKILL.md（规则 29 与 Process 之间）
  - ✅ 规则 32 加 Chinese-context exemption——豁免嵌入具体批评判断的格言体对举（接口 chinese-ai-tells 判别问 2 + 格言体对举谱系）
  - ✅ DETECTION GUIDANCE 加桥接句指向中文张晨腔 vs AI 腔判别框架
  - ✅ 英文规则计数 29→33（SKILL.md 3 处 + chinese-ai-tells.md 3 处）
  - ✅ version 2.5.1 → 2.8.0-zh（规则集对齐上游 v2.8.0 + 中文定制分支）
  - ⏳ 未移植（低优先，待后续）：规则 14 em/en dash 强化、规则 21 speculative gap-filling 补充、上游 Process 合并为 "Process and Output"（本地保留分开结构）；本地规则 13 Passive Voice 为定制保留（上游已删）
