# auto-mermaid

[English](#english) | [中文](#中文)

---

<a name="english"></a>

## English

**auto-mermaid** is an agent skill that turns vague diagram requests — especially *"maintain the diagrams for my repo"* — into a set of Mermaid diagrams grounded in real repository facts.

It covers the 24 chart types from the Mermaid Live Editor example menu and routes each piece of a scope to the type that fits its semantics, instead of forcing everything into one flowchart.

### What it does

- **Repository maintenance mode**: given only a scope (repo, directory, module, current diff), the skill inventories the code, splits it into readable slices, picks one or more best-fit chart types per slice, generates all diagram sources, and keeps a diagram atlas index with fact sources and coverage boundaries.
- **Explicit-type mode**: when you name chart types, they are honored; the skill still validates fit, generates from real facts, and states limits for ill-fitting types instead of silently swapping them.
- **Incremental maintenance**: untouched diagrams stay untouched; affected slices update; stale relations are removed only after confirmation.

### Covered chart types

Flowchart · Class · Sequence · Entity Relationship · State · Mindmap · Architecture · Block · C4 · Cynefin Framework · Event Modeling · Gantt · Git · Ishikawa · Kanban · Packet · Pie · Quadrant · Radar · Railroad (ABNF / EBNF / TIR / PEG) · Requirement

### Layout

```text
auto-mermaid/
├── SKILL.md                       # entry: triggers, modes, routing, hard rules
├── README.md                      # this file (bilingual)
└── references/
    ├── catalog.md                 # routing table: question -> chart type
    ├── repository-maintenance.md  # scanning, slicing, atlas, validation contract
    └── <24 chart-type references>
```

### Usage

Load `SKILL.md` as a skill, then make a request such as:

- *"maintain diagrams for this repo"* — full automatic mode
- *"add a sequence diagram for the checkout flow"* — explicit-type mode

The skill never claims a diagram passed validation unless it was actually rendered.

### Version note

Some types (Architecture, Cynefin, Event Modeling, Ishikawa, Radar, Packet, Railroad) have syntax that shifts across Mermaid versions. The skill treats the current Mermaid Live Editor example as the syntax authority before authoring those.

### License

MIT

---

<a name="中文"></a>

## 中文

**auto-mermaid** 是一个 agent 技能：把模糊的画图请求——尤其是那句"为我的仓库维护图"——变成一组基于真实仓库事实的 Mermaid 图。

它覆盖 Mermaid Live Editor 示例菜单的 24 种图表类型，按语义把范围内的每个片段路由到最合适的类型，而不是把所有东西硬塞进一张流程图。

### 能力

- **仓库图维护模式**：用户只给范围（仓库、目录、模块、当前改动），技能自动盘点代码、拆成可独立阅读的图片段、为每个片段选定一个或多个最适配类型、批量生成全部图源，并维护记录事实来源与覆盖边界的图册索引。
- **指定图表模式**：用户点名类型时按指定执行；技能仍负责范围拆解与事实生成，对不适配的类型明确报告限制，绝不静默换类型。
- **增量维护**：未受影响的图不动，受影响的只更新对应片段，失效关系确认后才删除。

### 覆盖的 24 种类型

Flowchart、Class、Sequence、Entity Relationship、State、Mindmap、Architecture、Block、C4、Cynefin Framework、Event Modeling、Gantt、Git、Ishikawa、Kanban、Packet、Pie、Quadrant、Radar、Railroad（ABNF / EBNF / TIR / PEG）、Requirement

### 结构

- `SKILL.md`：入口——触发条件、双模式、自动选型、硬规则
- `references/catalog.md`：路由表——"要回答的问题"对应图表类型
- `references/repository-maintenance.md`：仓库扫描、片段拆解、图册与验证契约
- `references/` 其余 24 个文件：各类型的适用场景、最小语法、规则与误用警示

### 使用

将 `SKILL.md` 作为技能加载后，直接说：

- "为这个仓库维护图" —— 全自动模式
- "给结账流程画一张时序图" —— 指定类型模式

未经实际渲染，技能不会声称任何图通过了校验。

### 版本说明

部分类型（Architecture、Cynefin、Event Modeling、Ishikawa、Radar、Packet、Railroad）的语法随 Mermaid 版本变化。技能在编写这些类型前，以当前 Mermaid Live Editor 官方示例作为语法权威。

### 许可

MIT
