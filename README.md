# book-to-skill-factory — 拆书 → 成课 → 成 Skill 生产链（方法论）

> 把一本书系统化加工为**三态资产**：学习档案（人读）→ 企业课程（人用）→ 可执行 Skill（Agent 用）。
> 本工作流来自 Question-to-Book OS 实战萃取（《销售就是会提问》全流程），整合开源最佳实践。

## 这是什么

一份可直接安装的 **Agent Skill**（playbook），教会任何支持 Agent Skills 的智能体（Claude Code / Codex / Reasonix 等）执行完整的"拆书成课成 Skill"生产链：

```
资料审计 → 决策卡(L0) → 知识地图(L1) → L2精读 → 学习档案落盘
→ 成课(体验式设计) → 成Skill(编译+路由) → 成果生产(Word/PPT/图示/陪练)
```

内含 **12 条实战踩坑**（PDF 中文提取 / edge-tts 声线限制 / 术语雷 / Word 表头渲染 / skill 安装限制等），避免其他智能体重复踩坑。

## 安装方法（给其他智能体）

**方式一：直接加载**（最简单）——将本仓库的 `SKILL.md` 放入智能体的 skills 目录：

```bash
# 例：Reasonix / Claude Code 项目级
<workspace>/.reasonix/skills/book-to-skill-factory/SKILL.md
```

**方式二：克隆仓库**：

```bash
git clone https://github.com/Atange2023/book-to-skill-factory.git
# 将 book-to-skill-factory/SKILL.md 复制到你的 skills 目录
```

安装后即可通过 `/book-to-skill-factory` 或 `run_skill({name: "book-to-skill-factory"})` 调用。

## 使用方法

向智能体提供：**书籍/资料文件 + 你的目标**（学到 L0–L5 哪一级、课程形态、Skill 用途）。

触发语示例：
- "拆这本书，做成课，再编译成 Skill"
- "用 factory 流程处理这份 PDF"

## 方法论家族（配套仓库）

本仓库是整个 skill 生态的**总纲**，与以下仓库构成家族（互链）：

| 仓库 | 角色 | 关系 |
| --- | --- | --- |
| [book-to-diagram-skill](https://github.com/Atange2023/book-to-diagram-skill) | 子能力：拆书 → 16:9 概论 SVG 图 | factory 阶段 7 引用 |
| [sales-roleplay-solo](https://github.com/Atange2023/sales-roleplay-solo) | 成品样例：数字人语音销售陪练系统 | factory 阶段 5 引用 |

## 依赖

- `pypdf`（PDF 提取，`py -m pip install pypdf`）
- `pandoc`（Word/文档转换）
- `edge-tts`（可选，语音陪练用）
- `python-pptx lxml`（可选，PPT 用）

## License

MIT © Anson TANG (atange2023)

## 版权与来源

方法框架源自《销售就是会提问》（青木毅，天津人民出版社 2021，引用标注页码）；本工作流为本项目原创，不包含原书正文。参考开源：anthropics/skills、agentskills、virgiliojr94/book-to-skill、apple-ouyang/book-to-skill。
