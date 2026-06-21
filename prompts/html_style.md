
### HTML 生成风格指南 (Morandi Style)

当需要将解读文档输出为 HTML 时，请使用以下规范生成单文件 HTML。

### 1. 设计理念：莫兰迪极简 (Morandi Minimalist)

- **核心色板**：低饱和度、高级灰调，营造沉静、专业的阅读氛围。
- **排版**：类似于 Medium 的沉浸式阅读体验，单栏布局，配合关键信息卡片。

---

### 2. CSS 样式规范

```css
:root {
    --bg-color: #FdfcF8;
    --text-main: #454545;
    --text-muted: #8c8c8c;
    --accent-blue: #8fa3ad;
    --accent-green: #9fb3a6;
    --accent-rust: #c4a29e;
    --card-bg: #f4f2ef;
    --code-bg: #f0f0f0;
    --border-radius: 8px;
}

* { box-sizing: border-box; }

body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    line-height: 1.9;
    color: var(--text-main);
    background-color: var(--bg-color);
    margin: 0;
    padding: 0;
}

.container {
    max-width: 800px;
    margin: 0 auto;
    padding: 40px 20px 80px;
}

/* ── 标题 ── */
h1, h2, h3 {
    font-weight: 600;
    margin-top: 2.2em;
    margin-bottom: 0.8em;
    letter-spacing: -0.02em;
}

h1 {
    font-size: 2.2em;
    color: var(--text-main);
    border-bottom: 4px solid var(--accent-blue);
    padding-bottom: 10px;
    display: inline-block;
}

h2 {
    font-size: 1.5em;
    color: var(--accent-blue);
    border-left: 4px solid var(--accent-blue);
    padding-left: 12px;
}

h3 {
    font-size: 1.15em;
    color: var(--accent-green);
}

p {
    margin-bottom: 1.5em;
    font-size: 1.05em;
}

/* ── 关键数字卡片（用于展示重要指标，如"提升 47%"）── */
.stat-cards {
    display: flex;
    gap: 16px;
    margin: 2em 0;
    flex-wrap: wrap;
}

.stat-card {
    flex: 1;
    min-width: 140px;
    background: #fff;
    border: 1px solid rgba(0,0,0,0.07);
    border-radius: var(--border-radius);
    padding: 20px 16px;
    text-align: center;
    box-shadow: 0 2px 12px rgba(0,0,0,0.04);
}

.stat-card .stat-number {
    font-size: 2em;
    font-weight: 700;
    color: var(--accent-blue);
    line-height: 1.1;
}

.stat-card .stat-label {
    font-size: 0.85em;
    color: var(--text-muted);
    margin-top: 6px;
}

/* ── 结论高亮块（用于"一句话结论"、"PM建议"等） ── */
.insight-box {
    background: linear-gradient(135deg, #eef2f0 0%, #f0ecea 100%);
    border-left: 4px solid var(--accent-green);
    border-radius: 0 var(--border-radius) var(--border-radius) 0;
    padding: 20px 24px;
    margin: 2.5em 0;
}

.insight-box .insight-label {
    font-size: 0.78em;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--accent-green);
    margin-bottom: 8px;
}

.insight-box p {
    margin: 0;
    font-size: 1.05em;
    font-weight: 500;
}

/* ── 警告/注意块（代价、风险、不适用场景） ── */
.warning-box {
    background: #fdf6f5;
    border-left: 4px solid var(--accent-rust);
    border-radius: 0 var(--border-radius) var(--border-radius) 0;
    padding: 16px 20px;
    margin: 2em 0;
}

.warning-box .warning-label {
    font-size: 0.78em;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--accent-rust);
    margin-bottom: 6px;
}

.warning-box p { margin: 0; font-size: 1em; }

/* ── 对比表格 ── */
.compare-table {
    width: 100%;
    border-collapse: collapse;
    margin: 2em 0;
    font-size: 0.95em;
}

.compare-table th {
    background: var(--card-bg);
    color: var(--text-main);
    font-weight: 600;
    padding: 12px 16px;
    text-align: left;
    border-bottom: 2px solid #ddd;
}

.compare-table td {
    padding: 10px 16px;
    border-bottom: 1px solid #ebebeb;
    vertical-align: top;
}

.compare-table tr:last-child td { border-bottom: none; }

.compare-table .tag-good {
    display: inline-block;
    background: #e8f0ed;
    color: #6a9180;
    font-size: 0.8em;
    padding: 2px 8px;
    border-radius: 20px;
}

.compare-table .tag-bad {
    display: inline-block;
    background: #f4e8e8;
    color: #a07070;
    font-size: 0.8em;
    padding: 2px 8px;
    border-radius: 20px;
}

/* ── 图片容器 ── */
.img-container {
    margin: 2.5em 0;
    text-align: center;
    background: #fff;
    padding: 20px;
    border-radius: var(--border-radius);
    box-shadow: 0 4px 20px rgba(0,0,0,0.03);
    border: 1px solid rgba(0,0,0,0.05);
}

.img-container svg { max-width: 100%; height: auto; }

.caption {
    margin-top: 12px;
    font-size: 0.88em;
    color: var(--text-muted);
    font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
}

/* ── 引用块 ── */
blockquote {
    background-color: var(--card-bg);
    border-left: 4px solid var(--accent-green);
    margin: 2em 0;
    padding: 1.2em 20px;
    font-style: italic;
    color: var(--text-main);
    border-radius: 0 var(--border-radius) var(--border-radius) 0;
}

/* ── 代码 ── */
pre {
    background-color: var(--code-bg);
    padding: 20px;
    border-radius: var(--border-radius);
    overflow-x: auto;
    font-size: 0.88em;
}

code {
    font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
    background-color: rgba(0,0,0,0.05);
    padding: 2px 5px;
    border-radius: 4px;
}

pre code { background-color: transparent; padding: 0; }

/* ── 列表 ── */
ul, ol { margin-bottom: 1.5em; padding-left: 20px; }
li { margin-bottom: 0.5em; }
li::marker { color: var(--accent-rust); }

strong { color: #2c3e50; font-weight: 700; }

hr { border: 0; height: 1px; background: #e0e0e0; margin: 4em 0; }

/* ── 移动端适配 ── */
@media (max-width: 600px) {
    .container { padding: 24px 16px 60px; }
    h1 { font-size: 1.7em; }
    h2 { font-size: 1.25em; }
    .stat-cards { flex-direction: column; }
    .stat-card { min-width: unset; }
    .compare-table { font-size: 0.85em; }
    .compare-table th, .compare-table td { padding: 8px 10px; }
}
```

---

### 3. 新增组件的 HTML 用法

**关键数字卡片**（放在 Phase 0 之后，展示1-3个最重要的指标）：
```html
<div class="stat-cards">
  <div class="stat-card">
    <div class="stat-number">+47%</div>
    <div class="stat-label">在 MATH-500 上超越前代</div>
  </div>
  <div class="stat-card">
    <div class="stat-number">1/10</div>
    <div class="stat-label">训练成本相比 GPT-4</div>
  </div>
</div>
```

**结论高亮块**（用于"PM视角总结"、"一句话建议"）：
```html
<div class="insight-box">
  <div class="insight-label">PM 视角</div>
  <p>如果你的产品需要多步推理（数学、代码、法律条文解析），这个技术值得现在就跟进；如果只是普通问答，现有方案已经够用。</p>
</div>
```

**注意/代价块**（用于风险、不适用场景）：
```html
<div class="warning-box">
  <div class="warning-label">注意</div>
  <p>推理速度比标准模型慢约 3 倍，实时响应场景要权衡体验。</p>
</div>
```

**对比表格**（用于新旧方案对比或选型建议）：
```html
<table class="compare-table">
  <tr><th>维度</th><th>旧方案</th><th>新方案</th></tr>
  <tr>
    <td>推理能力</td>
    <td><span class="tag-bad">较弱</span></td>
    <td><span class="tag-good">大幅提升</span></td>
  </tr>
  <tr>
    <td>响应速度</td>
    <td><span class="tag-good">快</span></td>
    <td><span class="tag-bad">慢 3×</span></td>
  </tr>
</table>
```

---

### 4. 输出要求

1. **完整性**：输出完整的 `<!DOCTYPE html>` 文档，CSS 直接内嵌在 `<head>` 的 `<style>` 中。
2. **SVG 内联**：将 SVG 图片内容直接写入 HTML，不使用 `<img src="...">` 外链。
3. **组件使用**：Phase 0 后必须有 stat-cards；Phase 4 的"一句话建议"必须用 insight-box 呈现。
4. **元数据**：自动提取论文标题作为 `<title>`，并在 `<header>` 区域显示论文来源/日期（如有）。
