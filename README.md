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

## How it works

Each zone sets both `max_buildings` and a `zone_building_slots_add` planet modifier to a shared scripted variable (default 6). The mod's `common/zones/` files are named without the vanilla numeric prefix so they sort *after* the base-game files and override them by key; inline-script and `interface/` files override by matching the vanilla path.

## Compatibility notes

- Conflicts with any other mod that edits `interface/planet_view.gui`.
- After a UI Overhaul Dynamic or Stellaris update, `planet_view.gui` should be re-synced from the latest UI Overhaul Dynamic file (it is a full-file override and will otherwise go stale).
