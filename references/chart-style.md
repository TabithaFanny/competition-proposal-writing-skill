# 图表生成规范 / Chart Style Guide

> 明确何时用Python生成图表、HTML单页生成、图表类型选择、输出目录和风格规范。

---

## 可视化三路分流规则

### 决策流程

```
发现可视化需求
     │
     ▼
┌─────────────────────────────────────┐
│ 核心信息是"精确数据"吗？              │
│ （数值比较、趋势、占比、预测）          │
└─────────────────────────────────────┘
     │是                    │否
     ▼                      ▼
Python matplotlib      ┌─────────────────────────────────────┐
                        │ 核心信息是"结构关系/流程逻辑"吗？     │
                        │ （架构图、流程图、闭环图、路线图）     │
                        └─────────────────────────────────────┘
                              │是                │否
                              ▼                  ▼
                        HTML单页            MiniMax图片生成
                        (assets/charts/)    (assets/images/)

```

### 第一路：Python matplotlib（数据图表）

**适用于：**
- 市场规模对比（TAM/SAM/SOM）
- 时间序列数据（历年增长趋势）
- 占比数据（收入结构、成本结构）
- 多维度对比（竞品分析矩阵）
- 预测数据（财务预测曲线）
- 用户增长趋势

**输出：** `assets/charts/*.png`

**规则：** 只要核心信息是"数值比较、趋势、比例"，优先走Python

---

### 第二路：HTML单页（结构图/流程图）

**适用于：**
- 商业模式图（平台模式、闭环结构）
- 服务流程图（用户旅程、业务闭环）
- 产品架构图（功能模块、平台关系）
- 路线图（战略里程碑、发展阶段）
- 组织架构图（团队结构、职能分工）
- 适合答辩展示的高视觉质量页面

**输出：** `assets/charts/*.html`

**规则：** 只要核心信息是"结构关系、流程逻辑、系统框架"，优先走HTML单页

**HTML单页规范：** 见 `html-prompt.md`

---

### 第三路：MiniMax图片生成（概念图/场景图）

**适用于：**
- 概念示意图（抽象概念的可视化）
- 产品mockup（界面示意图）
- 场景图（使用场景可视化）
- 需要视觉氛围但不依赖精确数据的图

**输出：** `assets/images/*.png`

**规则：** 只要核心信息不是精确数据也不是严格结构图，而是"概念展示/场景表达"，走图片生成

**状态：** 可选通道，API配置后启用

---

### 分流速查表

| 内容类型 | 方案 | 输出路径 |
|----------|------|----------|
| TAM/SAM/SOM规模 | Python | assets/charts/market/ |
| 市场增长率趋势 | Python | assets/charts/market/ |
| 收入/成本结构 | Python | assets/charts/financial/ |
| 竞品对比矩阵 | Python | assets/charts/competitors/ |
| 商业模式闭环 | HTML | assets/charts/business/ |
| 服务流程路径 | HTML | assets/charts/operation/ |
| 产品架构模块 | HTML | assets/charts/product/ |
| 战略里程碑 | HTML | assets/charts/operation/ |
| 概念示意 | MiniMax图片 | assets/images/ |
| 产品mockup | MiniMax图片 | assets/images/ |
| 场景图 | MiniMax图片 | assets/images/ |

---

## 何时启用Python

### 触发条件

当章节内容包含以下数据类型时，自动启用Python生成图表：

```
□ 市场规模对比（TAM/SAM/SOM）
□ 时间序列数据（历年增长）
□ 占比数据（收入结构、成本结构）
□ 多维度对比（竞品分析）
□ 预测数据（财务预测）
□ 用户增长趋势
```

### 不需要Python的情况
```
□ 数据点少于3个（手绘简单图即可）
□ 仅用于说明而非分析
□ 可以用表格代替
□ 评委更关注原始数据
```

---

## 图表类型选择规则

### 决策树

```
数据是什么类型？
│
├── 比较大小 → 柱状图 / 条形图
│   └── 若有层级关系 → 堆叠柱状图
│
├── 趋势变化 → 折线图
│   └── 若有多个系列 → 多线折线图
│
├── 占比组成 → 饼图 / 环形图
│   └── 若超过5个分类 → 环形图更清晰
│
├── 多维度对比 → 雷达图 / 矩阵图
│   └── 若维度超过6个 → 矩阵表更合适
│
├── 流程步骤 → 流程图
│
├── 时间节点 → 时间轴
│
├── 地理分布 → 地图热力图（复杂，一般不用）
│
└── 关系表达 → 组织图 / 架构图
```

### 图表类型优先级

| 场景 | 推荐图表 | 替代图表 |
|------|----------|----------|
| 市场规模TAM/SAM/SOM | 柱状图（分组） | 环形图 |
| 市场增长率 | 折线图 | 柱状图 |
| 竞品功能对比 | 矩阵图 | 雷达图 |
| 竞品多维度评分 | 雷达图 | 柱状图（分组） |
| 收入来源分布 | 饼图/环形图 | 堆叠柱状图 |
| 成本结构 | 饼图 | 环形图 |
| 用户画像 | 卡片式 | 标签云 |
| 发展里程碑 | 时间轴 | 流程图 |
| 融资用途分配 | 环形图 | 条形图 |
| 风险矩阵 | 矩阵图（2x2） | 表格 |
| 团队架构 | 组织图 | 层级列表 |
| 用户增长预测 | 折线图 | 面积图 |

---

## 输出目录结构

```
assets/charts/
├── market/
│   ├── tam-sam-som-[日期].png
│   ├── market-growth-[日期].png
│   └── market-share-[日期].png
├── competitors/
│   ├── competitor-matrix-[日期].png
│   └── competitor-radar-[日期].png
├── product/
│   └── product-architecture-[日期].png
├── financial/
│   ├── revenue-forecast-[日期].png
│   ├── cost-structure-[日期].png
│   ├── profit-trend-[日期].png
│   ├── cashflow-[日期].png
│   └── breakeven-[日期].png
├── team/
│   └── team-structure-[日期].png
├── operation/
│   ├── milestone-roadmap-[日期].png
│   └── user-growth-[日期].png
└── risk/
    └── risk-matrix-[日期].png
```

---

## 图表风格规范

### 配色方案

| 图表类型 | 主色 | 辅色 | 说明 |
|----------|------|------|------|
| 通用/默认 | #0066CC | #00A3E0 | 科技感 |
| 教育类 | #27AE60 | #2ECC71 | 绿色系 |
| 消费类 | #E67E22 | #F39C12 | 橙色系 |
| 公益类 | #16A085 | #1ABC9C | 青绿系 |
| 金融类 | #34495E | #7F8C8D | 专业灰 |

### 字体规范
```
标题：黑体/Arial Bold，14-16pt
标签：黑体/Arial，10-12pt
图例：黑体/Arial，10pt
单位：黑体/Arial，9pt
```

### 通用风格要求
```
□ 白底或浅灰底（#F8F9FA）
□ 颜色不超过3种
□ 留白充足
□ 标题清晰（说明图表主题）
□ 单位标注明确
□ 图例位置合理
□ 网格线淡化（灰色虚线）
□ 数据标签清晰可见
```

---

## Python图表生成模板

### 柱状图模板
```python
import matplotlib.pyplot as plt
import numpy as np

# 设置中文字体
plt.rcParams['font.sans-serif'] = ['Arial']
plt.rcParams['axes.unicode_minus'] = False

# 数据
categories = ['TAM', 'SAM', 'SOM']
values = [2760, 83, 2.5]  # 亿元
colors = ['#0066CC', '#00A3E0', '#5BA3D9']

# 绑图
fig, ax = plt.subplots(figsize=(8, 5))
bars = ax.bar(categories, values, color=colors, width=0.6)

# 标签
ax.set_ylabel('市场规模（亿元）', fontsize=12)
ax.set_title('市场规模估算（TAM/SAM/SOM）', fontsize=14, fontweight='bold')

# 数值标签
for bar, val in zip(bars, values):
    ax.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 30,
            f'{val}', ha='center', va='bottom', fontsize=11)

ax.set_ylim(0, max(values) * 1.2)
ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)

plt.tight_layout()
plt.savefig('assets/charts/market/tam-sam-som.png', dpi=150, bbox_inches='tight')
plt.close()
```

### 饼图模板
```python
import matplotlib.pyplot as plt

# 数据
labels = ['订阅收费', '硬件销售', '增值服务']
sizes = [70, 20, 10]
colors = ['#0066CC', '#00A3E0', '#5BA3D9']
explode = (0.05, 0, 0)

fig, ax = plt.subplots(figsize=(7, 7))
ax.pie(sizes, explode=explode, labels=labels, colors=colors,
       autopct='%1.0f%%', shadow=False, startangle=90,
       textprops={'fontsize': 12})
ax.set_title('收入结构预测（第3年）', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.savefig('assets/charts/financial/revenue-structure.png', dpi=150, bbox_inches='tight')
plt.close()
```

### 折线图模板
```python
import matplotlib.pyplot as plt

# 数据
years = [2024, 2025, 2026, 2027, 2028]
revenue = [120, 480, 1200, 2100, 3500]
profit = [30, 120, 360, 630, 1050]

fig, ax = plt.subplots(figsize=(9, 5))
ax.plot(years, revenue, marker='o', linewidth=2, color='#0066CC', label='收入')
ax.plot(years, profit, marker='s', linewidth=2, color='#27AE60', label='利润')

ax.set_xlabel('年份', fontsize=12)
ax.set_ylabel('金额（万元）', fontsize=12)
ax.set_title('收入与利润预测（2024-2028）', fontsize=14, fontweight='bold')
ax.legend(loc='upper left')
ax.grid(True, alpha=0.3)
ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)

plt.tight_layout()
plt.savefig('assets/charts/financial/revenue-profit-forecast.png', dpi=150, bbox_inches='tight')
plt.close()
```

---

## 图表命名规则

```
[类型]-[子类型]-[日期].png

示例：
- market-tam-sam-som-20240323.png
- financial-revenue-forecast-20240323.png
- competitor-radar-20240323.png
```

---

## 质量检查清单

生成图表后，必须检查：

```
□ 图表主题是否清晰
□ 标题是否说明核心结论
□ 颜色是否不超过3种
□ 数据标签是否清晰
□ 图例是否必要
□ 是否白底/浅底
□ 是否适合放进PPT（比例协调）
□ 中文是否正常显示
□ 导出格式是否为PNG（150dpi+）
```

---

## 与PPT的衔接

每张图表生成后，自动输出：

```
## 图表：market-tam-sam-som

### 图表文件
assets/charts/market/tam-sam-som-20240323.png

### 建议放于
[章节] 第X页：市场分析

### 讲稿建议
"如图所示，我们的目标市场分为三层：
TAM即潜在市场，2760亿元；
SAM即我们的可服务市场，83亿元；
SOM即我们的可获得市场，2.5亿元。"

### 图表风格确认
✅ 白底  ✅ 3色以内  ✅ 数据标签清晰  ✅ 中文正常
```
