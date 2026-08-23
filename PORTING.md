# 跨平台适配说明（PORTING）

本 skill 采用业界通用的 Agent Skills 形态（`SKILL.md` + YAML frontmatter + Markdown 正文），
可在大多数 agent 平台使用。以下为移植到其他平台时需调整的点。

## 一、目录放置

| 平台 | 放置目录 |
|---|---|
| DeepSeek Harness (DSH) | 项目 `<root>/.dsh/skills/ppt-production/` 或全局 `~/.dsh/skills/ppt-production/` |
| Claude Code | 项目 `.claude/skills/ppt-production/` 或 `~/.claude/skills/` |
| Cursor | `.cursor/skills/ppt-production/` |
| Codex | `~/.codex/skills/`（或按平台文档） |
| Gemini CLI | 按平台 skills 目录约定 |
| 其他 | 查平台文档中 SKILL.md 技能的放置路径 |

## 二、需替换的 DSH 特有内容

### 1. 提问工具
- **原文**：`用 ask_user_question 向用户提问，每轮不超过 4 个问题，优先给出选项 + 推荐项`
- **替换**：改为平台原生提问方式（多数平台直接在对话中提问，保留选项列表与推荐项标注即可）

### 2. 视觉分析工具（风格提取，Phase 0 第 3 步）
- **原文**：`用视觉分析工具（如 qwen_vision / describe_image）逐张分析主视觉与核心人物立绘`
- **替换**：改用平台的视觉/多模态能力（Claude 原生图像输入、Codex 截图分析、Gemini 原生视觉等），
  提取维度不变：色彩体系 / 绘画风格 / 构图版式 / 线条形状 / 质感特效 / 字体气质 / 装饰元素

### 3. 审美增强引用的外部 skill（可选）
- **原文**：加载 `hyperframes-creative`、`media-use`、`hyperframes` 系列
- **替换**：其他环境无这些 skill 时，将其降级为"设计方法论文字提示"（配色、排版、留白、素材处理原则），
  不影响门控流程主链路；若目标环境装有等价设计/素材 skill，可自行改名为对应技能。

### 4. 制作委托引擎
- **原文**：`vendor/ppt-master/`（hugohe3/ppt-master 工作流）+ python-pptx 通用能力
- **说明**：ppt-master 本身就是跨平台 skill（官方声明兼容任何 agent），在目标环境按其安装文档
  （`npx skills add` / 克隆 + pip）安装后，把本文件中 `vendor/ppt-master/` 路径改为目标环境实际路径；
  无 ppt-master 时自动退回 python-pptx 通用能力，流程不受影响。

## 三、完全通用、无需改动的部分

- 门控流程（Phase 0-4、门 A/B/C）
- 主题对象确认与按领域定制提问
- 美术素材必备（主视觉 + 核心人物立绘）与风格提取维度
- 文档产出（requirements / style-spec / outline）与模板
- 叙事主线大纲法、QA 清单、反思式复查
- 事实可信、占位符、跳过门记录等规则

## 四、快速检查清单（移植后）

- [ ] 新平台能发现 skill（目录正确、frontmatter 合法）
- [ ] 提问环节正常（无 ask_user_question 残留报错）
- [ ] 风格提取能看图（视觉工具可用）
- [ ] 制作委托路径指向目标环境的 ppt-master 或 python-pptx
- [ ] 找不到的外部 skill 引用已降级为文字说明
