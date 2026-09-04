# auto-mermaid

![badges](./assets/badges.png)

**一个 agent 技能：把模糊的画图请求——尤其是那句"为我的仓库维护图"——变成一组基于真实仓库事实的 Mermaid 图。**

[English README](./README.en.md) · [许可：MIT](./LICENSE)

![流水线](./assets/banner.png)

## 它解决什么问题

"画个图"是个模糊请求，常见的翻车姿势是一张巨大流程图加满虚构的箭头。`auto-mermaid` 的做法完全不同：

- 把请求当作**仓库图维护任务**，而不是单次画图
- 关系只从**真实证据**提取——源码符号、调用方、数据结构、状态机、配置、测试、Git 历史
- 没有**实际渲染**过，绝不声称某张图通过了校验

## 工作流程

1. **定范围** — 仓库、目录、模块、文件列表或当前改动。用户没给更窄的范围就取整仓，但先做轻量盘点；不会一次性读完所有源码。
2. **拆片段** — 范围切成可独立阅读的图片段；每段只回答**一个主要问题**（组件边界、调用路径、生命周期、数据关系、需求追溯、排期……）。
3. **路由类型** — 每段按语义路由到最适配的图表类型。完整路由表见 [`references/catalog.md`](./references/catalog.md)；一段出多张图只在"各回答独立问题且有独立事实支撑"时发生。
4. **生成** — 图源（`.mmd`）从对应类型参考文件的最小骨架起步，复用仓库词汇与稳定 ID，每条关系用 `%% facts` 注释留可追溯出处。
5. **验证** — 检查围栏块、声明、标识符、边方向、标签与事实出处，然后对每个块**用 `mmdc` 实际渲染**。
6. **维护** — 后续改动只更新受影响的片段；未受影响的图保持不动；失效关系确认后才删除；图册索引同步更新。

## 两种入口模式

| 模式 | 触发 | 行为 |
| --- | --- | --- |
| **仓库图维护** | 给了范围但没点名图表类型，如"为这个仓库维护图" | 完整流水线：盘点 → 拆段 → 自动路由 → 生成 → 建图册 |
| **指定类型** | 用户点名一个或多个图表类型 | 尊重用户指定；技能仍负责拆范围、检查适配，对不适配的类型**明确报告限制，绝不静默换类型** |

## 覆盖的图表类型

官方 Mermaid Live Editor examples 包的**全部 32 种**——每种一个独立参考文件（适用场景、官方默认示例作为语法权威、实测坑位）：

> Flowchart · Class · Sequence · Entity Relationship · State · Mindmap · Tree View · Architecture · Block · C4 · Cynefin Framework · Event Modeling · Gantt · Kanban · Git · Timeline · User Journey · Ishikawa · Wardley Maps · Packet · Requirement · Pie · Quadrant · Radar · XY Chart · Sankey · Treemap · Venn · Railroad（ABNF / EBNF / IR / PEG）

路由细节、组合规则与平局裁决见 [`references/catalog.md`](./references/catalog.md)。

## 共享样式目录

每个仓库只有**一份样式权威**：仓库根目录的 `.auto-mermaid/theme.css`。

- 渲染用 `mmdc -C .auto-mermaid/theme.css` 注入，`.mmd` 源保持**纯语义**——不写内联颜色、不做逐图样式
- 换样式只动**一个文件**加一轮重渲染；SVG 的 git diff 直接显示哪里变了
- [`references/repository-maintenance.md`](./references/repository-maintenance.md) 里的模板带**实测级联事实**（例如每条规则必须带 `#my-svg` ID 前缀，否则输掉 Mermaid 内嵌主题的级联）以及 CSS 控制边界（字体、线宽、圆角可以控，**节点位置控不了**）

## 仓库结构

```mermaid
%%{init: {'theme':'dark','themeCSS':'&{background-color:#0d1117}.treeView-node-label{fill:#e6edf3!important}.treeView-node-line{stroke:#8b949e!important}.treeView-node-icon{color:#8b949e!important}'}}%%
treeView-beta
auto-mermaid/
  LICENSE
  SKILL.md
  README.md
  README.en.md
  README.zh.md
  assets/
    banner.png
    badges.png
  references/
    catalog.md
    repository-maintenance.md
    architecture.md
    block.md
    c4.md
    class.md
    cynefin-framework.md
    entity-relationship.md
    event-modeling.md
    flowchart.md
    gantt.md
    git.md
    ishikawa.md
    journey.md
    kanban.md
    mindmap.md
    packet.md
    pie.md
    quadrant.md
    radar.md
    railroad-abnf.md
    railroad-ebnf.md
    railroad-ir.md
    railroad-peg.md
    requirement.md
    sankey.md
    sequence.md
    state.md
    timeline.md
    treemap.md
    treeview.md
    venn.md
    wardley.md
    xychart.md
```

## 硬规则（摘要）

- **事实优先。** 每条关系必须能追溯到文件、符号、文档、测试或 Git 记录；未知的标 pending，绝不编造。
- **渲染过才算数。** 图必须经过真实的 `mmdc` 渲染才能报告为通过校验；密集的图拆开画，不缩字号硬塞。
- **一份样式文件。** `.mmd` 源不写内联颜色；共享 `theme.css` 是唯一样式权威。

## 版本说明

多数类型为版本敏感（`-beta` 后缀或跨版本变动的语法）。每个参考文件内嵌的**官方默认示例**即当前语法权威；旧渲染器上渲染失败时，以该示例为准回查，而不是改源文件。

## 许可

[MIT](./LICENSE)
