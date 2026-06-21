# Paper Explainer Skill

将晦涩的 AI 论文，转化为产品经理也能看懂的图文研报。

## 这个 Skill 是给谁用的

**目标读者**：产品经理、运营、业务负责人——对 AI 感兴趣，但没有算法/工程背景。

它不做"学术翻译"，而是用讲故事的方式回答三个问题：
1. 这个技术在解决什么痛点？
2. 它怎么做到的？（用类比，不用公式）
3. 对我们的产品/业务意味着什么机会？

## 核心特性

- **故事化叙事**：从"旧方案有什么死穴"讲到"新突破怎么绕过去的"
- **PM 视角收尾**：每篇必须回答"业务场景、接入成本、产品机会点、选型建议"
- **视觉化解构**：自动生成极简 SVG 插图（优先 Before/After 对比图）
- **沉浸式研报**：莫兰迪配色 HTML 单文件，含关键数字卡片、结论高亮块、对比表格

## 使用方法

### 在 Claude Code、Cursor、Trae 或其他支持 Skill/Agent 的 IDE 中

1. 将此仓库放到项目的 `skills/` 目录下
2. 调用 `paper-explainer` skill
3. 提供论文（PDF、本地文本或 arXiv URL）
4. 输出：Markdown 解读 + 内联 SVG + 单文件 HTML 报告

### 手动使用

按顺序阅读以下文件，然后按 `SKILL.md` 的工作流执行：

| 文件 | 作用 |
|---|---|
| `SKILL.md` | 完整工作流，入口文件 |
| `prompts/narrative.md` | 叙事框架（五个 Phase） |
| `prompts/visual.md` | SVG 图表类型选择 + 绘制规范 |
| `prompts/html_style.md` | HTML/CSS 样式 + 组件用法 |

## 输出结构

```
output/
└── {paper_keyword}_report.html   # 单文件 HTML 报告（SVG 内联）
```

## 文件结构

```
.
├── SKILL.md                  # 工作流入口
├── prompts/
│   ├── narrative.md          # 叙事框架（Phase 0–4，PM 视角）
│   ├── visual.md             # SVG 绘制规范（含图表类型选择）
│   └── html_style.md         # HTML 样式（含数字卡片、高亮块等组件）
└── examples/
    └── full_workflow/
        ├── input/sample_paper.txt
        └── output_examples/
            ├── svg_samples/pipeline.svg
            └── html_samples/sample_report.html
```

## 依赖

- 图像生成：无（直接生成 SVG，不调用外部 API）
- URL 输入：需要 `WebFetch` / `WebSearch` 工具
- 本地 PDF：需要模型原生 PDF 读取能力

## 联系方式

wechat: PompeiiNeverStop

如有问题，欢迎提交 Issue。`prompts/` 下的文件可根据个人风格自由微调。

## 许可证

MIT License
