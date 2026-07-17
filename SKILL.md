---
name: user-research-console-design
description: "设计「用户研究预测引擎」类高端数据可视化网页的专门技能。当用户要构建用户研究 / 消费者洞察 / 预测仿真 / 多场景分析类可视化网页，或要求玻璃拟态、三色渐变(#00d4ff→#a855f7→#ff6b9d 135°)、暗亮主题、SVG 图标系统时调用。内含完整图标规范（禁用 emoji，改用 SVG sprite + 渐变描边）与参考实现页面。"
---

# 用户研究预测引擎 · 网页设计技能

## 这是什么

我们做过一个范例页面「用户研究预测引擎」(`user-research-console`)：玻璃拟态视觉 + 三色品牌渐变 + 多预测场景（新品上市 / 社媒活动 / 品类机会 / 新品创意可行性）+ ABM 多智能体仿真 + 加权公式双模型 + 多源数据直连校准，纯前端零后端。

本技能把它的设计语言沉淀为可复用规范，**重点是图标写法**——全部用 SVG sprite + 共享渐变，绝不用 emoji。

### 参考页面（必读，模仿对象）
- 线上：**https://ffswwwda.github.io/user-research-console/**
- 结构：左侧导航(9 项) + 顶栏(Logo / 主题切换 / 切引擎) + 概览 4 卡 + 预测工作台(场景切换 + 变量滑块 + 公式可调面板 + 数据源面板) + 数字世界 / 报告 / 基座 / 方法 / 架构页
- 随附演示：`references/icon-system.html`（独立可打开的图标系统，直接复制即用）

---

## 设计语言（硬约束）

### 配色
- **品牌渐变（全站统一，Logo / 图标 / 强调色都用它）**：
  ```css
  --grad: linear-gradient(135deg, #00d4ff 0%, #a855f7 50%, #ff6b9d 100%);
  ```
- **暗主题**：背景 `#0a0a16`~`#0d0d1f`；玻璃卡 `background:rgba(255,255,255,.04); backdrop-filter:blur(14px); border:1px solid rgba(255,255,255,.08)`
- **亮主题**：背景 `#f4f5fa`；玻璃卡 `rgba(10,10,30,.03)`，边框 `rgba(10,10,30,.08)`
- 文本：暗 `#e8e8f0` / 亮 `#1a1a2e`；次要文本降透明度
- 强调色统一取渐变里的中段 `#a855f7` 或末段 `#ff6b9d`，不要引入第四种主色

### 字体
系统字体栈；数字 / 指标用等宽 `font-variant-numeric:tabular-nums`

### 圆角与间距
卡圆角 14–18px；分节间距 28–40px；留白克制，不要堆砌

---

## 图标系统（核心 · 已按规范微调）

> **铁律：绝对不要用 emoji 当图标。** 全部用内联 SVG sprite + 共享渐变。

### 1. 在 `<body>` 开头注入 sprite（一次定义，全站 `<use>` 复用）

```html
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <linearGradient id="uiGrad" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0" stop-color="#00d4ff"/>
      <stop offset=".5" stop-color="#a855f7"/>
      <stop offset="1" stop-color="#ff6b9d"/>
    </linearGradient>
  </defs>
  <!-- 渐变描边图标（导航/卡/按钮/数据源），stroke=url(#uiGrad) -->
  <symbol id="i-grid" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><rect x="3" y="3" width="7" height="7" rx="1.6"/><rect x="14" y="3" width="7" height="7" rx="1.6"/><rect x="3" y="14" width="7" height="7" rx="1.6"/><rect x="14" y="14" width="7" height="7" rx="1.6"/></symbol>
  <symbol id="i-sliders" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><line x1="4" y1="8" x2="20" y2="8"/><circle cx="9" cy="8" r="2.4"/><line x1="4" y1="16" x2="20" y2="16"/><circle cx="15" cy="16" r="2.4"/></symbol>
  <symbol id="i-globe" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="12" cy="12" r="9"/><path d="M3 12h18"/><path d="M12 3a14 14 0 0 1 0 18 14 14 0 0 1 0-18z"/></symbol>
  <symbol id="i-gear" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M12 2v3M12 19v3M2 12h3M19 12h3M4.9 4.9l2.1 2.1M17 17l2.1 2.1M19.1 4.9 17 7M7 17l-2.1 2.1"/></symbol>
  <symbol id="i-doc" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M14 3H7a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8z"/><path d="M14 3v5h5"/><path d="M9 13h6M9 17h4"/></symbol>
  <symbol id="i-layers" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M12 3 3 8l9 5 9-5z"/><path d="M3 13l9 5 9-5"/></symbol>
  <symbol id="i-compass" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="12" cy="12" r="9"/><polygon points="15.5 8.5 11 11 8.5 15.5 13 13"/></symbol>
  <symbol id="i-build" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><rect x="4" y="3" width="16" height="18" rx="1.5"/><path d="M9 7h.01M15 7h.01M9 11h.01M15 11h.01M9 15h.01M15 15h.01M9 21v-3h6v3"/></symbol>
  <symbol id="i-bot" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><rect x="4" y="8" width="16" height="12" rx="2.5"/><path d="M12 8V4M9 4h6"/><circle cx="9.5" cy="14" r="1.2" fill="url(#uiGrad)"/><circle cx="14.5" cy="14" r="1.2" fill="url(#uiGrad)"/><path d="M9 18h6"/></symbol>
  <symbol id="i-steps" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M3 20h4v-5H3zM9 20h4V9H9zM15 20h4V4h-4z"/></symbol>
  <symbol id="i-zap" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><polygon points="13 2 4 14 11 14 11 22 20 10 13 10 13 2"/></symbol>
  <symbol id="i-users" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="9" cy="8" r="3.2"/><path d="M3.5 19c0-3 2.5-5 5.5-5s5.5 2 5.5 5"/><path d="M15.5 5.2a3.2 3.2 0 0 1 0 5.6"/><path d="M17 19c0-2.3-1.2-4.2-3-5"/></symbol>
  <symbol id="i-link" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M9 13a5 5 0 0 0 7 0l2-2a5 5 0 0 0-7-7l-1 1"/><path d="M15 11a5 5 0 0 0-7 0l-2 2a5 5 0 0 0 7 7l1-1"/></symbol>
  <symbol id="i-smile" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="12" cy="12" r="9"/><path d="M8.5 14.5c1 1.2 2.5 2 3.5 2s2.5-.8 3.5-2"/><path d="M9 9.5h.01M15 9.5h.01"/></symbol>
  <symbol id="i-flame" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M12 3c.5 3 3.5 4.5 3.5 8a3.5 3.5 0 0 1-7 0c0-1 .4-1.8 1-2.5C8.5 11 8 12.5 8 14a4 4 0 1 0 8 0c0-3.5-4-6-4-11z"/></symbol>
  <symbol id="i-clock" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="12" cy="12" r="9"/><path d="M12 7v5l3.5 2"/></symbol>
  <symbol id="i-share" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="18" cy="5" r="2.6"/><circle cx="6" cy="12" r="2.6"/><circle cx="18" cy="19" r="2.6"/><path d="M8.3 13.2 15.7 17.8M15.7 6.2 8.3 10.8"/></symbol>
  <symbol id="i-tag" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M20.6 13.4 12 22l-9-9V3h10z"/><circle cx="7.5" cy="7.5" r="1.4"/></symbol>
  <symbol id="i-bar" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M4 20h16"/><rect x="6" y="11" width="3" height="9" rx="1"/><rect x="11" y="6" width="3" height="14" rx="1"/><rect x="16" y="14" width="3" height="6" rx="1"/></symbol>
  <symbol id="i-plug" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M9 2v6M15 2v6"/><path d="M7 8h10v3a5 5 0 0 1-10 0z"/><path d="M12 16v6"/></symbol>
  <symbol id="i-target" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="5"/><circle cx="12" cy="12" r="1.6" fill="url(#uiGrad)"/></symbol>
  <symbol id="i-phone" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><rect x="7" y="2.5" width="10" height="19" rx="2.5"/><path d="M11 18.5h2"/></symbol>
  <symbol id="i-msg" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M21 11.5a8.5 8.5 0 0 1-12.5 7.4L3 21l2.2-5.2A8.5 8.5 0 1 1 21 11.5z"/></symbol>
  <symbol id="i-box" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M21 8 12 3 3 8v8l9 5 9-5z"/><path d="M3 8l9 5 9-5"/><path d="M12 13v8"/></symbol>
  <symbol id="i-trend" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><polyline points="3 17 9 11 13 15 21 7"/><polyline points="15 7 21 7 21 13"/></symbol>
  <symbol id="i-star" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><polygon points="12 3 14.5 9 21 9.4 16 13.6 17.8 20 12 16.4 6.2 20 8 13.6 3 9.4 9.5 9"/></symbol>
  <symbol id="i-moon" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M21 12.8A8.5 8.5 0 1 1 11.2 3 6.6 6.6 0 0 0 21 12.8z"/></symbol>
  <symbol id="i-sun" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2M2 12h2M20 12h2M4.9 4.9l1.4 1.4M17.7 17.7l1.4 1.4M19.1 4.9l-1.4 1.4M6.3 17.7l-1.4 1.4"/></symbol>
  <symbol id="i-swap" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><polyline points="17 3 21 7 17 11"/><path d="M21 7H7"/><polyline points="7 21 3 17 7 13"/><path d="M3 17h14"/></symbol>
  <symbol id="i-alert" viewBox="0 0 24 24" fill="none" stroke="url(#uiGrad)" stroke-width="2"><path d="M12 3 2 20h20z"/><path d="M12 9v5M12 17h.01"/></symbol>
  <!-- 白色图标（currentColor）：放在渐变底色方块上的品牌/流程/架构图标 -->
  <symbol id="w-fish" viewBox="0 0 24 24" fill="currentColor" stroke="none"><path d="M2 12c2.5-4 8-6 13-6 1.8 0 3.5.6 5 1.6L22 8v8l-2-1.6c-1.5 1-3.2 1.6-5 1.6-5 0-10.5-2-13-6z"/><circle cx="14" cy="11" r="1" fill="#1a1030"/></symbol>
  <symbol id="w-layers" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 3 3 8l9 5 9-5z"/><path d="M3 13l9 5 9-5"/></symbol>
  <symbol id="w-chip" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="6" y="6" width="12" height="12" rx="1.5"/><rect x="9" y="9" width="6" height="6" rx="1"/><path d="M9 2v3M15 2v3M9 19v3M15 19v3M2 9h3M2 15h3M19 9h3M19 15h3"/></symbol>
  <symbol id="w-wave" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M2 8c2 0 2 2 4 2s2-2 4-2 2 2 4 2 2-2 4-2 2 2 4 2"/><path d="M2 14c2 0 2 2 4 2s2-2 4-2 2 2 4 2 2-2 4-2 2 2 4 2"/></symbol>
  <symbol id="w-doc" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14 3H7a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8z"/><path d="M14 3v5h5"/><path d="M9 13h6M9 17h4"/></symbol>
  <symbol id="w-chat" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 12a8 8 0 0 1-11.6 7.1L3 21l1.9-6.4A8 8 0 1 1 21 12z"/></symbol>
  <symbol id="w-phone" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="7" y="2.5" width="10" height="19" rx="2.5"/><path d="M11 18.5h2"/></symbol>
  <symbol id="w-plug" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 2v6M15 2v6"/><path d="M7 8h10v3a5 5 0 0 1-10 0z"/><path d="M12 16v6"/></symbol>
  <symbol id="w-bar" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 20h16"/><rect x="6" y="11" width="3" height="9" rx="1"/><rect x="11" y="6" width="3" height="14" rx="1"/><rect x="16" y="14" width="3" height="6" rx="1"/></symbol>
</svg>
```

### 2. 配套 CSS

```css
.ic-svg{display:inline-block;vertical-align:middle;flex-shrink:0;stroke-linecap:round;stroke-linejoin:round;fill:none}
.brand-logo svg{width:22px;height:22px;color:#fff}              /* 品牌 Logo：白鱼 + 渐变方块 */
.side-item .ic{width:18px;height:18px}                          /* 侧栏导航 */
.stat-label .ic-svg{width:16px;height:16px}                    /* 统计卡标签 */
.flow-ic svg{width:28px;height:28px;color:var(--ts)}           /* 流程步骤（--ts=渐变） */
.ds-ic{width:38px;height:38px;border-radius:10px;background:rgba(255,255,255,.06);display:flex;align-items:center;justify-content:center}
.ds-ic svg{width:20px;height:20px}                             /* 数据源面板 */
.arch-ic svg{width:26px;height:26px;color:#fff}                /* 架构卡（白图标 + 渐变底） */
```

### 3. 用法

```html
<!-- 渐变描边图标 -->
<svg class="ic-svg"><use href="#i-globe"/></svg>
<!-- 白色图标（放在 .arch-ic 这类渐变底容器里） -->
<div class="arch-ic"><svg><use href="#w-fish"/></svg></div>
```

### 图标规则（微调要点）
- **UI 图标（导航 / 卡 / 按钮 / 数据源）**：`stroke="url(#uiGrad)"` 三色渐变描边，细线 `stroke-width="2"`，Lucide / Feather 风格（克制几何）。
- **放在渐变底色方块上的图标（品牌 Logo / 流程步骤 / 架构卡）**：白色 `fill="currentColor" stroke="none"`，且所在容器 `color:#fff` + 渐变背景，保证对比度。
- **命名**：渐变版 `i-xxx`、白版 `w-xxx`；新增图标沿用 `24×24` viewBox、`2px` 描边、简洁几何。
- ⚠️ **切换主题 / 重渲染的 JS 绝不能用 `el.textContent = …` 覆盖图标节点**，否则 SVG 变文字或空白；改图标要用 `innerHTML` 或直接操作 `<use>` 的 `href`。
- ⚠️ 渐变描边图标**必须有 `<linearGradient id="uiGrad">` 定义**，否则所有描边渲染成黑色。
- 校验：上线前 `grep` 全文件确认无 emoji 残留（🐟📊🤖 等），且每个 `<use href="#x">` 都能在 sprite 里找到对应 `<symbol id="x">`。

---

## 架构模式（这类网页的通用骨架）

1. **场景化**：`SCENES` 配置 + `SCENE_DEFAULTS`（种子 / 问题 / 市场基线随场景联动，切换场景要刷新所有联动控件）。
2. **变量面板**：滑块 / 开关 → 写入 `dataset`，实时联动图表。
3. **预测引擎**：确定性仿真（种子化伪随机 `mulberry32`，同参数可复算）+ 加权公式双轨；公式关键参数**暴露为 UI 可调**（权重 / 校准系数 / 上帝变量加成 / 活动抬升）。
4. **数据源系统**：`DATA_SOURCES` 数组，每个含 `handler` 类型、`scenes` 推荐映射、远程 `url`、`accuracy` 档位；直连后调用对应 `parseXxx` 重算基线；准确率档位 `L0–L3` 实时指示。
5. **报告页**：按场景提取专属 KPI + 图表 + 填数结论模板（不同目的输出不同结果）。
6. **主题与 favicon**：暗 / 亮切换；favicon 用三色渐变小鱼（`assets/favicon.svg`）。

---

## 避坑清单

- 不要默认暗色 / 野兽派（除非用户明确要）；用户偏好「干净亮色 + 克制」。
- 预测指标（如爆款率）**不要**用变量连乘破百（如 ×5 次），用**加法叠加 + 校准系数封顶**，默认给合理中值（如 73%），全拉满 + 活动才到 100%。
- 图标**绝不用 emoji**（见图标系统）。
- JS 重渲染不要把 SVG 图标覆盖回 emoji。
- 远程数据源 URL 指向真实可达地址；跨仓库文件若不可推送，优先放本仓库并改 URL，避免 404 断链。

---

## 参考资源

- **线上范例**：https://ffswwwda.github.io/user-research-console/
- `references/icon-system.html`：独立可打开的图标系统演示，直接复制即用
- `assets/favicon.svg`：三色渐变小鱼 favicon 源码
