# user-research-console-skill

设计「用户研究预测引擎」类高端数据可视化网页的 WorkBuddy 技能。

## 它能做什么

把我们在 `user-research-console` 项目里沉淀的设计语言固化成可复用规范，让 AI 在构建同类网页（用户研究 / 消费者洞察 / 预测仿真 / 多场景分析）时直接套用：

- 玻璃拟态 + 三色品牌渐变（`#00d4ff→#a855f7→#ff6b9d` 135°）的统一视觉
- 暗 / 亮主题切换
- **图标系统（重点）**：全部用 SVG sprite + 共享渐变，**绝不用 emoji**
- 场景化架构、变量面板、预测引擎、数据源系统、报告页的通用骨架
- 避坑清单（不连乘破百、不默认暗色野兽派、JS 重渲染不覆盖 SVG 等）

## 目录结构

```
user-research-console-skill/
├── SKILL.md                    # 技能主体（设计语言 + 架构 + 图标规范 + 参考页面）
├── references/
│   └── icon-system.html        # 独立可打开的图标系统演示，直接复制即用
├── assets/
│   └── favicon.svg             # 三色渐变小鱼 favicon 源码
└── README.md
```

## 参考页面

线上范例：**https://ffswwwda.github.io/user-research-console/**

## 使用

把本仓库放入 WorkBuddy 技能目录（用户级 `~/.workbuddy/skills/` 或项目级 `.workbuddy/skills/`），对话中用中文描述「做一个用户研究 / 预测类可视化网页」即可被路由命中。

## 图标写法（一句话）

`<body>` 开头注入一段 `<svg>` sprite（含 `<linearGradient id="uiGrad">` 和若干 `<symbol>`），UI 图标用 `stroke="url(#uiGrad)"` 渐变描边，放在渐变方块上的图标用白色 `currentColor`；使用时 `<svg class="ic-svg"><use href="#i-xxx"/></svg>`。绝不写 emoji。
