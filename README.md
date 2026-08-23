# ppt-grill — 门控式 PPT 制作流程规划 Skill

> 仓库名 ppt-grill，skill 名 `ppt-production`（frontmatter 中 name 字段）。

一个门控式 PPT 制作流程规划 skill：**先问清需求 → 素材到位 → 风格提取确认 → 大纲确认 → 验证页确认 → 委托制作 → 验收交付**。纯规划定位，不直接生成演示文件。

## 核心流程（五阶段、三道确认门）

```
Phase 0 需求澄清与风格提取 ─门A─▶ Phase 1 大纲与整体需求 ─门B─▶ Phase 2 验证页(1-2页) ─门C─▶ Phase 3 整体制作 ─▶ Phase 4 QA验收与交付
```

- **门 A**：需求清单 + 风格草案确认（含素材缺口清单）
- **门 B**：大纲与视觉规范确认
- **门 C**：验证页风格确认（可迭代）

## 特点

- **主题对象确认先行**：先弄清 PPT 主题是游戏/小说/产品等，再按领域定制提问（游戏问玩法、小说问剧情、产品问卖点）
- **美术素材必备**：用户须提供一张主视觉 + 数张核心人物立绘，用视觉分析提取美术风格（色彩/画风/版式/字体气质）并确认，风格不凭空设计
- **纯规划 + 委托制作**：产出需求清单、风格草案、大纲与制作规格，实际生成文件委托外部能力（ppt-master / python-pptx / hyperframes / media-use），本 skill 负责规格与验收
- **跨平台**：Agent Skills 标准形态，适配说明见 [PORTING.md](./PORTING.md)

## 文件结构

```
SKILL.md        skill 主体（流程、门控、规则）
templates/      需求清单 / 风格草案 / 大纲 / QA 清单 模板
PORTING.md      跨平台适配说明
```

## 安装

- **DeepSeek Harness (DSH)**：将本目录放入项目 `.dsh/skills/ppt-production/` 或全局 `~/.dsh/skills/ppt-production/`
- **其他平台**：见 [PORTING.md](./PORTING.md)（Claude Code / Cursor / Codex / Gemini CLI 等）

## 使用

新开会话直接说："帮我做一份关于 X 的 PPT"，并准备主视觉 + 核心人物立绘素材。
