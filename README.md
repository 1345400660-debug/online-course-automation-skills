# online-course-automation-skills

在线课程作业自动化技能集：把「智慧树答题」与「中国大学 MOOC 单元测验」两类高频任务，沉淀为可复用的
WorkBuddy 技能（Skill）。每个技能用标准 `SKILL.md` 描述**用途、适用场景、输入、执行步骤**，并把平台
实测的操作经验放到 `references/`，便于跨会话、跨课程复用。

> 仓库名：`online-course-automation-skills`

## 技能总览

| 技能 | 目录 | 一句话用途 |
| --- | --- | --- |
| 智慧树在线答题 | `skills/zhihuishu-quiz/` | 自动完成智慧树（知到）知识点练习/单元测试/AI 测评，按题干匹配答案、批量填答、提交计分、写回进度断点 |
| 中国大学 MOOC 单元测验 | `skills/mooc-quiz/` | 自动完成 MOOC 各周单元测验，逐题作答、全卷复核、提交并回看答卷，沉淀按题干归档的答案库 |

### 1. zhihuishu-quiz（智慧树在线答题）

- **用途**：完成智慧树课程「必学」与「知识点练习 / 提升掌握度」，按题干匹配答案、批量填答、切题保存、查漏、提交并读取评分，最少 token 完成一轮。
- **适用场景**：走完必学、各知识点各练一轮、重刷掌握度 <70% 的知识点、接续上一会话未完成任务。
- **输入**：课程入口 URL、已登录浏览器、`智慧树课程进度.json` 断点、可选题目缓存。
- **执行步骤**：恢复连接 → 读断点 → 进入练习 → 读 DOM 定位题号选项 → 按题干填答 → 切回第 1 题查漏 → 提交并读评分 → 写回 `quizAudit`/`graphStatus` 并简短回报。

### 2. mooc-quiz（中国大学 MOOC 单元测验）

- **用途**：完成 MOOC 各周单元测验（15 题 / 满分 30 / 3 次提交取最高），逐题作答、全卷复核、提交并回看答卷核对，答案按题干归档。
- **适用场景**：逐周完成单元测验、题序选项随机打乱时按内容作答、提交出错后评估重刷、沉淀答案库。
- **输入**：assessments 页面 URL、目标周次与截止时间、已登录浏览器、可选答案库。
- **执行步骤**：展开周次 → 开始测验 → 逐题作答（单点单截图）→ 填空两步法 → 全卷复核 → 提交 → 回看答卷 → 写答案库。

## 目录结构

```
online-course-automation-skills/
├── README.md                        # 本文件：技能总览 + 目录结构 + 发布方式
├── CHANGELOG.md                     # 版本变更记录
├── VERSION                          # 版本号
├── .gitignore
├── skills/
│   ├── zhihuishu-quiz/
│   │   ├── SKILL.md                 # 技能主文档（用途/场景/输入/步骤）
│   │   └── references/
│   │       └── experience.md        # 智慧树平台实测经验与坑
│   └── mooc-quiz/
│       ├── SKILL.md                 # 技能主文档（用途/场景/输入/步骤）
│       └── references/
│           └── experience.md        # MOOC 平台实测经验与纪律
└── docs/
    └── PUBLISHING.md                # 发布与更新方式说明
```

## 安装 / 使用

1. 把 `skills/zhihuishu-quiz/`、`skills/mooc-quiz/` 目录复制到
   `~/.workbuddy/skills/`（用户级，跨项目可用）或项目 `.workbuddy/skills/`（项目级共享）。
2. 也可通过 WorkBuddy 的「安装技能」搜索安装对应的 `skill`。
3. 触发：直接对 WorkBuddy 说「帮我做智慧树这章的知识点练习」或「帮我做这门 MOOC 第 X 周单元测验」即可。

## 发布方式

见 [`docs/PUBLISHING.md`](docs/PUBLISHING.md)。
