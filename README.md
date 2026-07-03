# Simple More District Building Slots (4.4.x)

A Stellaris mod that gives each planet zone **6** building slots (capital / city zone: **12**) instead of the vanilla 3.

## Credit & attribution

This mod is an **independent reimplementation inspired by** the original **简单更多区划建筑槽位** ("Simple More District Building Slots"). The slot logic here was **rewritten from scratch** — current vanilla zones with a single shared inline script — rather than copied from the original.

The **user interface**, however, is **derived from the original author's mod**: `interface/planet_view.gui` reuses their expanded building-slot grid layout, layered on UI Overhaul Dynamic. Credit for that layout is theirs.

- **Original mod (Steam Workshop):** https://steamcommunity.com/sharedfiles/filedetails/?id=3479726947

Not affiliated with or endorsed by the original author.

## Requirements

- **[UI Overhaul Dynamic](https://steamcommunity.com/sharedfiles/filedetails/?id=1623423360)** — load this mod **after** it. This mod overrides UI Overhaul Dynamic's `interface/planet_view.gui`.

## How it works

The target is **6** building slots per zone (vanilla 3, doubled). Slot count comes from a `planet_modifier { zone_building_slots_add }`, which the engine **sums** across a zone's inline scripts — so the top-up differs by what each zone already inherits from vanilla. Two shared inline scripts cover the cases:

- **`shared_add_building_slots_6.txt`** — `max_buildings = 6` + `zone_building_slots_add = 6`. Used by the **44** zones that have **no** building-slot grant of their own.
- **`shared_add_building_slots_3.txt`** — `max_buildings = 6` + `zone_building_slots_add = 3`. Used by the **98** zones that already inherit `zone_building_slots_add = 3` from a vanilla productive shared script (`shared_energy_zone`, `shared_minerals_zone`, …). 3 (vanilla) + 3 = **6**.
- **`shared_add_building_slots_5.txt`** — `max_buildings = 6` + `zone_building_slots_add = 5`. Used by the **2** hive spawning zones (`zone_spawning`, `zone_spawning_hive`), which inherit only `zone_building_slots_add = 1` from `shared_spawning_zone`. 1 + 5 = **6**.

The `common/zones/~smbs-*` files are the vanilla zone definitions with the right one of these inserted into each zone, and the vanilla `max_buildings` / `zone_building_slots_add` literals stripped. The `~smbs-` prefix sorts them **last of all**: `~` (0x7E) sorts after `z`, so these files load after vanilla **and** after any `zz_` / `zzzz_`-style zone mod, winning the per-key override. `common/zones/` resolves duplicate zone keys by **filename order**, not launcher load order — which is why a plain `zz_` prefix lost to `zz_nullcore_*`.

The sole exception is `zone_default` (capital / city), which keeps its own `max_buildings = 12` and imports nothing (vanilla 6, doubled).

`interface/planet_view.gui` is a full-file override that widens the building-slot grid so the extra slots render.

## Compatibility notes

- Conflicts with any other mod that edits `interface/planet_view.gui`.
- After a UI Overhaul Dynamic or Stellaris update, `planet_view.gui` should be re-synced from the latest UI Overhaul Dynamic file (it is a full-file override and will otherwise go stale).
- After a major Stellaris update, re-sync the `common/zones/~smbs-*` files from current vanilla and re-insert the inline-script line into each zone — `shared_add_building_slots_3` for zones that inherit a vanilla `zone_building_slots_add` from a productive shared script, `shared_add_building_slots_5` for the spawning zones (vanilla +1), `shared_add_building_slots_6` for those that inherit nothing (keeping `zone_default` at 12). The shared inline scripts themselves rarely need touching.

---

# 中文说明

一个 Stellaris Mod，让每个行星区划提供 **6** 个建筑槽位（首都 / 城市区划为 **12** 个），而非原版的 3 个，使每颗星球能容纳更多建筑。

## 致谢

本 Mod 是一个**受原作启发、独立重写**的实现，灵感来源于原 Mod **简单更多区划建筑槽位**。其中的槽位逻辑是**从零重写**的（采用当前原版区划 + 单个共享内联脚本），而非直接拷贝原作。

但**用户界面**则**沿用自原作者的 Mod**：`interface/planet_view.gui` 复用了他扩展后的建筑槽位格子布局，并叠加在 UI Overhaul Dynamic 之上。该布局的功劳归原作者所有。

- **原 Mod（Steam 创意工坊）：** https://steamcommunity.com/sharedfiles/filedetails/?id=3479726947

本 Mod 与原作者无关，也未经其认可。

## 前置需求

- **[UI Overhaul Dynamic](https://steamcommunity.com/sharedfiles/filedetails/?id=1623423360)** —— 必需，并将本 Mod 的加载顺序放在它**之后**。本 Mod 会覆盖 UI Overhaul Dynamic 的 `interface/planet_view.gui`。

## 工作原理

目标是每个区划 **6** 个建筑槽位（原版 3，翻倍）。槽位数来自 `planet_modifier { zone_building_slots_add }`，而游戏引擎会把一个区划中多个内联脚本的该修正**相加**，因此补足量取决于该区划已从原版继承了多少。两个共享内联脚本覆盖了所有情况：

- **`shared_add_building_slots_6.txt`** —— `max_buildings = 6` + `zone_building_slots_add = 6`。用于那 **44** 个本身没有任何建筑槽位加成的区划。
- **`shared_add_building_slots_3.txt`** —— `max_buildings = 6` + `zone_building_slots_add = 3`。用于那 **98** 个已从原版“产出型”共享脚本（`shared_energy_zone`、`shared_minerals_zone` 等）继承了 `zone_building_slots_add = 3` 的区划。3（原版）+ 3 = **6**。
- **`shared_add_building_slots_5.txt`** —— `max_buildings = 6` + `zone_building_slots_add = 5`。用于那 **2** 个蜂巢产卵区划（`zone_spawning`、`zone_spawning_hive`），它们仅从 `shared_spawning_zone` 继承了 `zone_building_slots_add = 1`。1 + 5 = **6**。

`common/zones/~smbs-*` 文件是原版区划定义，在每个区划中插入了对应的那个脚本，并删除了原版的 `max_buildings` / `zone_building_slots_add` 字段。`~smbs-` 前缀（`~` 编码 0x7E，排在 `z` 之后）使这些文件排在**最后**：位于原版以及任何 `zz_` / `zzzz_` 类前缀的区划 Mod 之后，从而赢得按键覆盖。`common/zones/` 按**文件名顺序**（而非启动器加载顺序）解析重复区划键，故前缀才是决定因素——这也是普通 `zz_` 会输给 `zz_nullcore_*` 的原因。

唯一的例外是 `zone_default`（首都 / 城市区划），它保留自身的 `max_buildings = 12`，且不引入任何脚本（原版 6，翻倍）。

`interface/planet_view.gui` 为整文件覆盖，加宽了建筑槽位格子布局，使额外的槽位得以显示。

## 兼容性

- 与其他修改 `interface/planet_view.gui` 的 Mod 冲突。
- 在 UI Overhaul Dynamic 或 Stellaris 更新后，应基于最新的 UI Overhaul Dynamic 文件重新同步 `planet_view.gui`（它是整文件覆盖，否则会过时）。
- 在 Stellaris 大版本更新后，应基于当前原版重新同步 `common/zones/~smbs-*` 文件，并把内联脚本那一行重新插入每个区划 —— 对于从原版“产出型”共享脚本继承了 `zone_building_slots_add` 的区划用 `shared_add_building_slots_3`，产卵区划（原版 +1）用 `shared_add_building_slots_5`，其余无继承的用 `shared_add_building_slots_6`（首都 `zone_default` 保持 12）。共享内联脚本本身通常无需改动。
