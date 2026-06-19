# Simple More District Building Slots — community 4.4.x update

Original mod: **简单更多区划建筑槽位** ("Simple More District Building Slots").

A Stellaris mod that gives each planet zone **6** building slots (capital / city zone: **12**) instead of the vanilla 3.

## Credit & attribution

This repository is a **community-made compatibility update**. All credit for the original mod goes to its creator.

- **Original mod (Steam Workshop):** https://steamcommunity.com/sharedfiles/filedetails/?id=3479726947

This repository contains only a 4.4.x compatibility / bug-fix update of the above. It is not affiliated with or endorsed by the original author.

## Requirements

- **[UI Overhaul Dynamic](https://steamcommunity.com/sharedfiles/filedetails/?id=1623423360)** — load this mod **after** it. This mod overrides UI Overhaul Dynamic's `interface/planet_view.gui`.

## What this update changes

- Adds the 6 / 12 building slots to the new Nomad "arkship" / Forever Cruise zones (`common/zones/arkshipZones.txt` plus the overridden shared inline scripts under `common/inline_scripts/zones/`).
- Rebuilds `interface/planet_view.gui` from the **current** UI Overhaul Dynamic file — fixing a 4.4.2 crash on arkship/Nomad planets (the old copy was missing the new arkship UI) and restoring the 3×4 (city) / 3×2 (other) building-slot grid layout.
- Re-synced all `common/zones/` files and the slot-bearing `common/inline_scripts/zones/` scripts from current 4.4 vanilla — clearing stale-copy load errors (`has_planet_flag` scope, removed/renamed modifiers) and dropping the old `z_my*` redirect layer.

## How it works

Each zone sets both `max_buildings` and a `zone_building_slots_add` planet modifier to a shared scripted variable (default 6). The mod's `common/zones/` files are named without the vanilla numeric prefix so they sort *after* the base-game files and override them by key; inline-script and `interface/` files override by matching the vanilla path.

## Compatibility notes

- Conflicts with any other mod that edits `interface/planet_view.gui`.
- After a UI Overhaul Dynamic or Stellaris update, `planet_view.gui` should be re-synced from the latest UI Overhaul Dynamic file (it is a full-file override and will otherwise go stale).
- The `common/zones/` files and slot-bearing `common/inline_scripts/zones/` scripts are full-file overrides too — they conflict with other mods editing the same zones, and should likewise be re-synced from vanilla after a major Stellaris update (re-copy, then re-apply `max_buildings` / `zone_building_slots_add = @TINYGROX_MAX_BUILDINGS`, capital `zone_default` = 12).

---

# 中文说明

原 Mod：**简单更多区划建筑槽位**。

一个 Stellaris Mod，让每个行星区划提供 **6** 个建筑槽位（首都 / 城市区划为 **12** 个），而非原版的 3 个，使每颗星球能容纳更多建筑。

## 致谢

本仓库是一个**社区制作的兼容性更新**。原 Mod 的全部功劳归于其作者。

- **原 Mod（Steam 创意工坊）：** https://steamcommunity.com/sharedfiles/filedetails/?id=3479726947

本仓库仅包含上述 Mod 的 4.4.x 兼容性 / 修复更新，与原作者无关，也未经其认可。

## 前置需求

- **[UI Overhaul Dynamic](https://steamcommunity.com/sharedfiles/filedetails/?id=1623423360)** —— 必需，并将本 Mod 的加载顺序放在它**之后**。本 Mod 会覆盖 UI Overhaul Dynamic 的 `interface/planet_view.gui`。

## 本次更新内容

- 为新增的游牧“方舟” / 永恒航行（Forever Cruise）区划补上了 6 / 12 建筑槽位（`common/zones/arkshipZones.txt` 以及 `common/inline_scripts/zones/` 下被覆盖的共享内联脚本）。
- 基于**当前版本**的 UI Overhaul Dynamic 文件重建了 `interface/planet_view.gui` —— 修复了 4.4.2 打开方舟 / 游牧行星时的崩溃（旧文件缺少新增的方舟界面元素），并恢复了城市 3×4 / 其他 3×2 的建筑格子布局。
- 将所有 `common/zones/` 文件以及含槽位字段的 `common/inline_scripts/zones/` 脚本基于**当前 4.4 原版**重新同步 —— 清除了旧文件导致的载入报错（`has_planet_flag` 作用域、被移除/改名的修正），并移除了旧的 `z_my*` 重定向层。

## 工作原理

每个区划都会把 `max_buildings` 与 `zone_building_slots_add` 行星修正设为一个共享脚本变量（默认 6）。本 Mod 的 `common/zones/` 文件不带原版的数字前缀，因此排序在原版文件**之后**并按键覆盖；内联脚本与 `interface/` 文件则通过匹配原版路径进行覆盖。

## 兼容性

- 与其他修改 `interface/planet_view.gui` 的 Mod 冲突。
- 在 UI Overhaul Dynamic 或 Stellaris 更新后，应基于最新的 UI Overhaul Dynamic 文件重新同步 `planet_view.gui`（它是整文件覆盖，否则会过时）。
- `common/zones/` 文件与含槽位字段的 `common/inline_scripts/zones/` 脚本同样是整文件覆盖 —— 会与其他修改相同区划的 Mod 冲突，并应在 Stellaris 大版本更新后同样从原版重新同步（重新拷贝，再把 `max_buildings` / `zone_building_slots_add` 改回 `@TINYGROX_MAX_BUILDINGS`，首都 `zone_default` 为 12）。
