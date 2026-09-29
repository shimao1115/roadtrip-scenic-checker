# roadtrip-scenic-checker

一个面向**混动城市 SUV 自驾游客**的 Qoder / Claude 系 Agent Skill。它会驱动模型用检索工具实时核实景点信息，并按固定的十项检查表输出一份目的地分析报告。

## 它解决什么问题

普通旅游类提示词最容易出的问题是**幻觉**：编造门票价格、编造餐厅、把历史训练数据当成"现在开放"。这个技能把"必须实时检索、查不到就明说无法核实"设为高于格式的硬约束，并且要求每个事实段落附来源。

## 输出结构（十条）

1. 背景底蕴 — 历史由来、特产、非遗、全国/省级文物保护单位
2. 票务与开放（实时检索）— 开放状态、准确票价、预约与限流
3. 混动城市 SUV 路况评估 — 拥堵、铺装比例、托底风险、补能、停车、限行
4. 核心看点与观赏指南
5. 最佳观景点与摄影指南
6. 景区避雷点（结合近期反馈）
7. 周边美食 — 仅推荐地图上真实存在且营业的具体店铺
8. 真实口碑星级 — 1–5 星，严苛评分，附优缺点
9. 收费景点性价比 — 1–5 星，含计算口径
10. 老幼同行便利度 — **仅当用户明确提到老人/孩子同行时才输出**

报告末尾固定附「未核实清单」，提示出发前电话确认。

## 安装

### Qoder IDE / CLI

```bash
npx skills add shimao1115/roadtrip-scenic-checker -a qoder
```

或手动放置：

```
~/.qoder/skills/roadtrip-scenic-checker/SKILL.md      # 用户级，所有项目可用
<项目根>/.qoder/skills/roadtrip-scenic-checker/SKILL.md  # 项目级，覆盖同名用户级
```

国内版 CLI 目录为 `~/.qoder-cn/skills/`，QoderWork 为 `~/.qoderwork/skills/`。
放置后开新会话自动加载；已在运行的 CLI 可执行 `/skills reload`。

### 其他支持 Agent Skills 的环境

Claude Code、Codex 等同样读取 `<skill-name>/SKILL.md` 结构，把 `skills/roadtrip-scenic-checker/` 拷进对应的 skills 目录即可。

## 使用

装好后三种触发方式：

- **自动**：直接报地名，例如「成都新都区」「国庆去袁家界怎么样」
- **斜杠**：输入 `/` 选择技能，或直接 `/roadtrip-scenic-checker`
- **指名**：「用 roadtrip-scenic-checker 分析 XX」

想让第 10 条生效，明确写出「带 70 岁老人」「有 3 岁小孩要推婴儿车」。

## 已知限制

- 小红书、大众点评、高德 App 的正文通常无法直接抓取。相关结论会基于可获取的公开来源，并在报告中注明来源受限、样本偏小。
- 门票与开放时间随时变动，报告里的价格请以景区当日公示为准。

## 文件

```
skills/roadtrip-scenic-checker/SKILL.md
```
