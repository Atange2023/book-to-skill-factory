---
name: book-to-skill-factory
description: 拆书→成课→成Skill端到端生产链经验萃取版：审计→L0-L2→档案→课程→Skill，含踩坑清单
---

---
name: book-to-skill-factory
description: 拆书→成课→成Skill 端到端生产链（经验萃取版）：资料审计→L0-L2拆解→学习档案→课程→可执行Skill，全程来源锚定
---

# book-to-skill-factory — 拆书成课成 Skill 生产链（经验萃取 v1）

把一本书（或课程资料）系统化加工为三态资产：**学习档案**（人读）→ **企业课程**（人用）→ **可执行 Skill**（Agent 用）。本工作流来自 Question-to-Book OS 实战验证（《销售就是会提问》全流程拆解），整合开源最佳实践（virgiliojr94/book-to-skill 15k★、apple-ouyang/book-to-skill、anthropics/skills 官方仓库、agentskills 规范）。

## 触发条件
- 收到书籍/PDF/课程资料，用户要求"拆书、做成课、做成 Skill"。
- 已有学习档案，需要"编译为可执行 Skill"或"设计企业课程"。

## 所需输入
- 书籍/资料文件（PDF/EPUB/DOCX）；用户目标（学到 L0–L5 哪一级、课程形态、Skill 用途）
- 工具：`py`（Windows Python launcher）+ `pypdf`（PDF 提取）、`pandoc`、`edge-tts`（可选语音）

## 工作流（七阶段）

### 阶段 0 · 资料审计（先解决"能不能读"）
1. 提取顺序：`pdftotext` → 中文为 0 时改用 `pypdf`（calibre 转换 PDF 的 ToUnicode 损坏常见，pypdf 可救）。
2. **判断乱码必须看 UTF-8 文件而非控制台**（Windows 控制台 GBK 会把正常中文显示成乱码）。
3. 验证：中文字符数 >0 且 U+FFFD=0；记录页数/ISBN/作者。
4. 登记 `SOURCE_REGISTER.md`；无法读取的图片/公式/扫描页显式声明（不假装已读）。

### 阶段 1–2 · 决策卡（L0）→ 知识地图（L1）
- 决策卡：问题/读者/承诺/结构/作者/增量/偏见/精读-选读-略读/不确定性（`BOOK_TRIAGE_TEMPLATE`）。
- 知识地图：结构树 + 核心命题清单 + 与用户体系接口 + 待深读清单，全部标页码。

### 阶段 3 · L2 精读（支撑一切产出的地基）
- 概念卡（原文定义/自己的解释/正例反例/来源位置）+ 命题—证据矩阵（S1–S4 分级）。
- **无数据断言标 `[S4 待核实]`**（如"90% 客户需要被提问"），对外内容不采用或显式标注。
- 技巧/方法类做速查卡（一条一行 + 页码锚定）。

### 阶段 4 · 学习档案落盘
`11_learning/books/<书名>/`：简报/决策卡/知识地图/概念卡/命题矩阵/速查卡/改写示例/原文提取底稿 + 索引（INDEX.md）。

### 阶段 5 · 成课（企业课程）
- 用 `enterprise-course-design` 设计课程（方案/目标/模块/评估/课件说明）。
- **行为改变类课程用体验式设计**：沙盘/角色扮演（Kolb 循环：体验→反思→概括→再实验；Pfeiffer & Jones 五阶段 + 引导师 5 问）。讲授占比 ≤25%。
- 沙盘要点：3 人组（销售/客户/观察者）、角色卡含隐藏需求、轮次递进、三维度评分、失败阈值（红线 2 次/关键节点 3 次）、通关/失败统一复盘（含理论出处）。
- 参考：`question-selling` 可执行 Skill + 数字人语音陪练（edge-tts，多角色）。

### 阶段 6 · 成 Skill（编译）
按 `book-to-skill` 元技能：
1. 框架抽取：每个框架标 名称/触发场景/Use X when Y/反模式。
2. 可执行化：执行步骤（Agent 可直接执行）+ 真实案例（S1 锚定）+ 验证标准。
3. 分层编译：主 `SKILL.md`（常驻 ≤4K tokens，含路由表）+ `references/<框架>.md`（按需）+ glossary/patterns/cheatsheet。
4. 路由：主 Skill 判断场景 → 指向 references 文件。
5. 版权检查：只合成转述+短引用，不复制原文段、不对外发布"某书 Skill"。

### 阶段 7 · 成果生产
文章（`serious-chinese-writing` + `anti-ai-style-editor`）、图示（`book-to-diagram` SVG 16:9）、Word（标准模板+fix_tables）、PPT（`mck-ppt-design` 咨询风）、陪练系统（剧本+台词库+TTS）。

## 经验教训（踩坑清单，务必遵守）

| 坑 | 对策 |
| --- | --- |
| pdftotext 提不出中文 | 用 pypdf；写 UTF-8 文件验证（不靠控制台） |
| edge-tts 中文男声仅 4 个（Yunjian/Yunxi/Yunxia/Yunyang） | 不存在的 voice 报 NoAudioReceived；查可用列表再配 |
| edge-tts rate 需带符号（`-8%`/`+0%`，`0%` 报错） | 统一 +/- 前缀 |
| TTS 批量偶发限流 | speak() 内置 3 次退避重试 |
| 对客户讲术语（如"SKILLS 技能库"）→"听不懂" | 翻译成生活比喻（"像手机 App"） |
| 交换式条件（"报名才给体验课"）触发防御 | 先给善意再谈流程（书原则 1：先帮助） |
| Word 表头条件样式不渲染（显示白色） | fix_tables.py 直接写单元格 shd（#4472C4 白字） |
| dashi-ppt goal 校验严（长度预算/数量平衡） | 一次脚本难通过；用 mck-ppt-design（本地 python-pptx）或交互打磨 |
| install_source 20MB 限制 / auto 识别失败 | 大 skill 手动复制到 `.reasonix/skills/<name>/`；description ≤120 字符 |
| 文档被 Word 占用无法覆盖 | 输出新文件名 |

## 输出
- 三态资产：学习档案 / 课程方案（含 Word/PPT 交付）/ 可执行 Skill（.reasonix/skills/）
- 复盘的关卡系统（剧本/台词库/语音/复盘报告）

## 验收标准
1. 每个结论可回原文页码（S1–S4 分级标注）；
2. 学习档案完整（11 件套+INDEX）；
3. Skill 有路由表 + 每框架有执行步骤和可溯源案例；
4. 交付物（Word/PPT）走系统缺省排版；
5. 无大段原文、无虚构数据。

## 适用边界
- 方法论/框架型书籍收益最大；纯叙事/文学书不适用。
- 只处理用户自有副本；爬虫/OCR/转写等缺口显式声明（不硬凑）。
- 承诺边界：Skill 是决策辅助，不承诺"照做必成"。

## 失败处理
- 提取失败 → 报原因给方案（换源/OCR），不伪造内容。
- 校验不过（dashi/Skill 编译）→ 降级（文字模式/简化流程/交互打磨）。
- 客户不买账（课程场景）→ 复盘归因（术语/交换式/未挖动机），重打。

## 配套资产（本系统已验证）
- 模板：`08_style/word模板_微软雅黑.docx` + `fix_tables.py`；PPT 用 `mck-ppt-design` 引擎
- 参考开源：virgiliojr94/book-to-skill、apple-ouyang/book-to-skill、anthropics/skills（166k★）、agentskills/agentskills（23k★）
- 实战样例：question-selling（可执行 Skill）、《销售就是会提问》完整档案、sales-roleplay-solo（GitHub 公开）

## 版本
v1（2026-08-03）· 由 Question-to-Book OS 实战萃取 · 供其他智能体同步开展工作
