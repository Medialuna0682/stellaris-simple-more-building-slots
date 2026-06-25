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

- A single shared inline script — `common/inline_scripts/zones/shared_add_building_slot_modifiers.txt` — supplies `max_buildings = 6` plus a `planet_modifier { zone_building_slots_add = 6 }`.
- The `common/zones/zz_*` files are the vanilla zone definitions with that inline script inserted into **each** zone, and the vanilla `max_buildings` / `zone_building_slots_add` literals stripped so the shared values take over. The `zz_` prefix sorts them **after** the base-game files, so they override the matching zones by key.
- `zone_default` (the capital / city zone) is the **sole exception**: it keeps its own `max_buildings = 12` and does **not** import the shared script (vanilla 6, doubled).
- `interface/planet_view.gui` is a full-file override that widens the building-slot grid so the extra slots render.

## Compatibility notes

- Conflicts with any other mod that edits `interface/planet_view.gui`.
- After a UI Overhaul Dynamic or Stellaris update, `planet_view.gui` should be re-synced from the latest UI Overhaul Dynamic file (it is a full-file override and will otherwise go stale).
- After a major Stellaris update, re-sync the `common/zones/zz_*` files from current vanilla and re-insert the shared inline-script line into each zone (keeping `zone_default` at 12). The shared inline script itself rarely needs touching.

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

- 单个共享内联脚本 —— `common/inline_scripts/zones/shared_add_building_slot_modifiers.txt` —— 提供 `max_buildings = 6` 以及 `planet_modifier { zone_building_slots_add = 6 }`。
- `common/zones/zz_*` 文件是原版区划定义，在**每个**区划中插入了该内联脚本，并删除了原版的 `max_buildings` / `zone_building_slots_add` 字段，从而由共享值生效。`zz_` 前缀使这些文件排序在原版文件**之后**，按键覆盖对应区划。
- `zone_default`（首都 / 城市区划）是**唯一例外**：保留自身的 `max_buildings = 12`，且**不**引入共享脚本（原版 6，翻倍）。
- `interface/planet_view.gui` 为整文件覆盖，加宽了建筑槽位格子布局，使额外的槽位得以显示。

## 兼容性

- 与其他修改 `interface/planet_view.gui` 的 Mod 冲突。
- 在 UI Overhaul Dynamic 或 Stellaris 更新后，应基于最新的 UI Overhaul Dynamic 文件重新同步 `planet_view.gui`（它是整文件覆盖，否则会过时）。
- 在 Stellaris 大版本更新后，应基于当前原版重新同步 `common/zones/zz_*` 文件，并把共享内联脚本那一行重新插入每个区划（首都 `zone_default` 保持 12）。共享内联脚本本身通常无需改动。
