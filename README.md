# book-to-skill-factory v1.2

把一本书或长篇 PDF 转化为四类可复用资产：学习档案、金句/案例/版本素材库、课程与可执行 Skill，以及面向书籍目标读者的响应式“拆书精要”网页。

## v1.2 新增

- 目标读者两步推导：先判断书籍目标读者，再结合当前分享场景收窄；
- E 路线“读者分享版”：单文件、离线、响应式 HTML；
- 原句、编辑改写、S1-S4 与 E1-E3 的发布边界；
- 内容源与呈现层分离，支持结构化测试；
- 1440px 桌面端与 390px 手机端浏览器真实渲染验收；
- `agents/openai.yaml`，便于 Codex 等支持 Agent Skills 的工具发现与调用。

## 生产链

```text
来源与版本审计 → L0 决策卡 → L1 知识地图 → L2 精读
→ 金句库 / 案例库 / 版本谱系 → 学习档案
→ 成课 → 成 Skill → 读者分享版 → 验收
```

## 安装

请安装完整目录，不要只复制 `SKILL.md`；v1.2 会按任务读取 `references/` 中的证据、金句、案例、版本和网页发布规范。

```text
book-to-skill-factory/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── case-library-spec.md
    ├── edition-comparison-spec.md
    ├── evidence-and-source.md
    ├── output-manifest.md
    ├── quote-library-spec.md
    └── reader-first-html-spec.md
```

将完整目录放入运行时的 skills 目录，例如：

```text
<workspace>/.reasonix/skills/book-to-skill-factory/
~/.codex/skills/book-to-skill-factory/
~/.agents/skills/book-to-skill-factory/
```

也可以克隆本仓库后复制完整目录：

```bash
git clone https://github.com/Atange2023/book-to-skill-factory.git
```

## 使用示例

- “拆解这本书，先做 A 路线快速验收。”
- “补齐金句库和案例库，并标明引用边界。”
- “比较新版与旧版，整理有证据等级的再版亮点。”
- “基于全部研究成果生成面向本书目标读者的响应式拆书精要网页。”

## 相关项目

- [book-to-diagram-skill](https://github.com/Atange2023/book-to-diagram-skill)：书籍内容到可视化图示；
- [sales-roleplay-solo](https://github.com/Atange2023/sales-roleplay-solo)：课程与数字人陪练成品样例。

## License

MIT © Anson TANG (Atange2023)

