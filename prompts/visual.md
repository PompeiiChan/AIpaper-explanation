### SVG 图像生成规范

当需要为技术概念生成解释图时，请编写简洁、优雅的 SVG 代码。

---

### 0. 面向非技术读者：先选对图表类型

在动笔之前，先判断"这个技术概念用什么图最容易让PM看懂"：

| 场景 | 推荐图表类型 | 避免 |
|---|---|---|
| 解释"旧方案 vs. 新方案的差异" | **Before/After 对比图**（左右分栏） | 纯流程图 |
| 解释"这个系统有几个模块" | **方块组合图**（模块+简短标签） | UML类图 |
| 解释"数据怎么流转" | **线性流程图**（从左到右，5步以内） | 复杂网状图 |
| 解释"这个技术比别人好在哪" | **柱状对比图**或**雷达图** | 表格罗列 |
| 解释"训练/推理的逻辑" | **循环/迭代示意图** | 数学符号图 |

**原则**：每张图只讲一件事。宁可画两张简单的图，也不要把五个概念塞进一张图。

---

### 1. 核心画风：极简科技线稿

- **视觉参照**：Notion 风格插画、Excalidraw 风格。
- **SVG 参数规范**：
    - `width="800"` `height="400"` (保持 2:1 比例；Before/After 图可用 `height="320"`)
    - `viewBox="0 0 800 400"`
    - `xmlns="http://www.w3.org/2000/svg"`
- **样式定义 (`<style>`)**：
    ```css
    .line { fill: none; stroke: #333; stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; }
    .dashed { stroke-dasharray: 5,5; }
    .text { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; font-size: 14px; fill: #454545; }
    .label-sm { font-size: 12px; fill: #8c8c8c; }
    .highlight { stroke: #8fa3ad; stroke-width: 3; }   /* 雾霾蓝高亮 */
    .accent { fill: #9fb3a6; stroke: none; opacity: 0.2; }  /* 灰豆绿背景块 */
    .old-style { fill: #f4e8e8; stroke: #c4a29e; stroke-width: 1.5; } /* 旧方案：暖红调 */
    .new-style { fill: #e8f0ed; stroke: #9fb3a6; stroke-width: 1.5; } /* 新方案：绿调 */
    ```

---

### 2. Before/After 对比图模板（优先使用）

这是最适合非技术受众的图表类型。左边画"旧方案"，右边画"新方案"，中间用对比符号分隔。

```xml
<svg width="800" height="320" viewBox="0 0 800 320" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto" markerUnits="strokeWidth">
      <path d="M0,0 L0,6 L9,3 z" fill="#333" />
    </marker>
  </defs>
  <rect width="100%" height="100%" fill="#ffffff" />

  <!-- 左侧：旧方案 -->
  <text x="190" y="40" text-anchor="middle" class="text" style="font-weight:600;fill:#c4a29e;">旧方案</text>
  <!-- 在此处绘制旧方案内容 -->

  <!-- 中间分隔 -->
  <line x1="400" y1="30" x2="400" y2="290" stroke="#e0e0e0" stroke-width="1" stroke-dasharray="4,4" />
  <text x="400" y="168" text-anchor="middle" style="font-size:28px;fill:#8c8c8c;">→</text>

  <!-- 右侧：新方案 -->
  <text x="610" y="40" text-anchor="middle" class="text" style="font-weight:600;fill:#9fb3a6;">新方案</text>
  <!-- 在此处绘制新方案内容 -->
</svg>
```

---

### 3. 线性流程图模板

适合"数据流转"或"步骤顺序"类的概念，步骤不超过5步。

```xml
<svg width="800" height="400" viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto" markerUnits="strokeWidth">
      <path d="M0,0 L0,6 L9,3 z" fill="#333" />
    </marker>
  </defs>
  <rect width="100%" height="100%" fill="#ffffff" />

  <!-- 步骤1 -->
  <rect x="60" y="160" width="120" height="80" rx="8" class="line" fill="#f4f2ef" />
  <text x="120" y="196" text-anchor="middle" class="text">步骤1</text>
  <text x="120" y="214" text-anchor="middle" class="label-sm">简短说明</text>

  <!-- 连线：从步骤1右边界到步骤2左边界 -->
  <line x1="180" y1="200" x2="240" y2="200" class="line" marker-end="url(#arrow)" />

  <!-- 步骤2 -->
  <rect x="240" y="160" width="120" height="80" rx="8" class="line" fill="#f4f2ef" />
  <text x="300" y="196" text-anchor="middle" class="text">步骤2</text>
  <text x="300" y="214" text-anchor="middle" class="label-sm">简短说明</text>
</svg>
```

---

### 4. 连线布局规则（防止"箭头乱插"）

1. **锚点在边界**：连线起点/终点必须是图形的边缘坐标，不能是中心。
   - 矩形 `x=100, y=100, w=80, h=40`：右锚点 `(180, 120)`，左锚点 `(100, 120)`
   - 圆形 `cx=200, cy=200, r=40`：右锚点 `(240, 200)`，左锚点 `(160, 200)`

2. **绕开遮挡**：连线不能穿过文本或矩形内部，用贝塞尔曲线 `Q x1 y1, x y` 绕行。

3. **文字间距**：线条与文本之间保留至少 15px 安全间距。

4. **箭头不伸进去**：`marker-end` 箭头尖端应刚好触碰目标边缘，终点坐标往回缩 8px。

5. **连线长度**：主流程水平连线保持 40-80px，避免出现"5px短箭头"或"横穿全图"。
