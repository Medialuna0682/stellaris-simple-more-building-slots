# Simple More District Building Slots (4.4.x)

A Stellaris mod that gives each planet zone **6** building slots (capital / city zone: **12**) instead of the vanilla 3.

## Credit & attribution

This mod is an **independent reimplementation inspired by** the original **简单更多区划建筑槽位** ("Simple More District Building Slots"). The slot logic here was **rewritten from scratch** — current vanilla zones with `max_buildings` set directly — rather than copied from the original.

The **user interface**, however, is **derived from the original author's mod**: `interface/planet_view.gui` reuses their expanded building-slot grid layout, layered on UI Overhaul Dynamic. Credit for that layout is theirs.

- **Original mod (Steam Workshop):** https://steamcommunity.com/sharedfiles/filedetails/?id=3479726947

Not affiliated with or endorsed by the original author.

## Requirements

- **[UI Overhaul Dynamic](https://steamcommunity.com/sharedfiles/filedetails/?id=1623423360)** — load this mod **after** it. This mod overrides UI Overhaul Dynamic's `interface/planet_view.gui`.

## How it works

A zone's building-slot count is its `max_buildings` (vanilla 3). The mod sets `max_buildings = 6` directly on every zone, doubling the grid to **6**. `zone_default` (capital / city) is the exception, kept at **12**.

The `common/zones/~~smbs-*` files are the vanilla zone definitions with each zone's `max_buildings` set to 6. The `~~smbs-` prefix sorts them **last of all**: `~` (0x7E) sorts after `z`, so these files load after vanilla **and** after any `zz_` / `zzzz_`-style zone mod, winning the per-key override. `common/zones/` resolves duplicate zone keys by **filename order**, not launcher load order — which is why a plain `zz_` prefix lost to `zz_nullcore_*`.

**Why only `max_buildings`:** an earlier version also set `zone_building_slots_add` via a *separate* `planet_modifier` block. But a zone effectively honours only one `planet_modifier` — a second block silently discards the first block's other modifiers, which wiped every specialized zone's production (the volatile-motes / rare-crystal / research conversions, etc.). `max_buildings` alone drives the buildable count, so that is all we set. *(Cosmetic note: the tooltip's "building slots +N" line still reports the vanilla `zone_building_slots_add`, so it under-reports versus the real `max_buildings = 6`.)*

`interface/planet_view.gui` is a full-file override that widens the building-slot grid so the extra slots render.

## Compatibility notes

- Conflicts with any other mod that edits `interface/planet_view.gui`.
- After a UI Overhaul Dynamic or Stellaris update, `planet_view.gui` should be re-synced from the latest UI Overhaul Dynamic file (it is a full-file override and will otherwise go stale).
- After a major Stellaris update, re-sync the `common/zones/~~smbs-*` files from current vanilla: set `max_buildings = 6` on every zone except `zone_default` (which stays `max_buildings = 12`). Do **not** add `zone_building_slots_add` — see "How it works".

---

# 中文说明

一个 Stellaris Mod，让每个行星区划提供 **6** 个建筑槽位（首都 / 城市区划为 **12** 个），而非原版的 3 个，使每颗星球能容纳更多建筑。

## 致谢

本 Mod 是一个**受原作启发、独立重写**的实现，灵感来源于原 Mod **简单更多区划建筑槽位**。其中的槽位逻辑是**从零重写**的（采用当前原版区划，直接设置 `max_buildings`），而非直接拷贝原作。

但**用户界面**则**沿用自原作者的 Mod**：`interface/planet_view.gui` 复用了他扩展后的建筑槽位格子布局，并叠加在 UI Overhaul Dynamic 之上。该布局的功劳归原作者所有。

- **原 Mod（Steam 创意工坊）：** https://steamcommunity.com/sharedfiles/filedetails/?id=3479726947

本 Mod 与原作者无关，也未经其认可。

## 前置需求

- **[UI Overhaul Dynamic](https://steamcommunity.com/sharedfiles/filedetails/?id=1623423360)** —— 必需，并将本 Mod 的加载顺序放在它**之后**。本 Mod 会覆盖 UI Overhaul Dynamic 的 `interface/planet_view.gui`。

## 工作原理

每个区划的建筑槽位数即其 `max_buildings`（原版 3）。本 Mod 直接把每个区划的 `max_buildings` 设为 **6**，使格子翻倍。`zone_default`（首都 / 城市区划）为例外，保持 **12**。

`common/zones/~~smbs-*` 文件是原版区划定义，把每个区划的 `max_buildings` 改为 6。`~~smbs-` 前缀（`~` 编码 0x7E，排在 `z` 之后）使这些文件排在**最后**：位于原版以及任何 `zz_` / `zzzz_` 类前缀的区划 Mod 之后，从而赢得按键覆盖。`common/zones/` 按**文件名顺序**（而非启动器加载顺序）解析重复区划键，故前缀才是决定因素——这也是普通 `zz_` 会输给 `zz_nullcore_*` 的原因。

**为何只改 `max_buildings`：** 早期版本还通过*另一个* `planet_modifier` 块设置 `zone_building_slots_add`。但一个区划实际只认一个 `planet_modifier` —— 第二个块会静默丢弃第一个块的其他修正，从而抹掉各专精区划的产出（易爆微粒 / 稀有水晶 / 研究转化等）。实际可建槽位由 `max_buildings` 决定，故只设它即可。*（提示：工具提示中的“建筑槽位 +N”仍显示原版 `zone_building_slots_add`，因此低于真实的 `max_buildings = 6`。）*

`interface/planet_view.gui` 为整文件覆盖，加宽了建筑槽位格子布局，使额外的槽位得以显示。

## 兼容性

- 与其他修改 `interface/planet_view.gui` 的 Mod 冲突。
- 在 UI Overhaul Dynamic 或 Stellaris 更新后，应基于最新的 UI Overhaul Dynamic 文件重新同步 `planet_view.gui`（它是整文件覆盖，否则会过时）。
- 在 Stellaris 大版本更新后，应基于当前原版重新同步 `common/zones/~~smbs-*` 文件：把除 `zone_default`（保持 `max_buildings = 12`）以外每个区划的 `max_buildings` 设为 6。**不要**添加 `zone_building_slots_add`（原因见“工作原理”）。
