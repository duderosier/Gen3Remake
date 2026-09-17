<div align="center">

# Gen 3 Remake

**A ROM-accurate Pokémon Emerald engine, rebuilt from scratch in Lua.**

Runs on Android and desktop · Reads everything from *your* Emerald cartridge dump · Moddable with plain Lua files

[**Download the demo**](../../releases/latest) · [Wiki](../../wiki) · [FAQ](../../wiki/FAQ) · [Report a bug](../../issues)

`alpha` · `LÖVE 11.5` · `Android / Windows / macOS / Linux` · `no ROM included`

</div>
<p align="center"><img src="docs/demo.gif" width="720" alt="Gen 3 Remake demo"></p>


## What this is

Gen 3 Remake is a fan-made engine that plays Pokémon Emerald the way the original does, with the original data,
using a modern runtime instead of a GBA emulator.

- **Nothing is bundled.** Sprites, maps, tilesets, music, fonts, dialogue, species, moves, items, trainers, and
  scripts are read from your own Pokémon Emerald (USA/Europe) ROM while you play. The download is code only.
- **Checked against the source.** Overworld behaviour, event scripts, menus, and the battle system are verified
  against the [pret/pokeemerald](https://github.com/pret/pokeemerald) decompilation, byte by byte where it matters.
- **Built to be modded.** Drop a Lua file in a folder and it can change dialogue, encounters, gifts, cutscenes, and
  more. No rebuild, no ROM patching, no engine source needed.

## The demo

The current public demo covers the opening of the adventure:

> **Littleroot Town → Routes 101–104 → Oldale → Petalburg → Petalburg Woods → Rustboro City (Roxanne) →
> Rusturf Tunnel → Mr. Briney → Dewford Town (Brawly) → Granite Cave → Route 109 → Slateport City**

It ends when you deliver the **DEVON GOODS to Capt. Stern** at the Oceanic Museum. Everything past Slateport is locked.

| Included | |
|---|---|
| Story events and side quests | ROM-accurate item gifts, item balls, and hidden items |
| Trainers and the first two Gyms | Wild encounters and fishing |
| Pokémon Centers, Poké Marts, PC storage | Pokédex, PokéNav, Bag, Trainer Card, saving |
| Touch controls on Android | Keyboard or gamepad on desktop |

## Get started

**You need your own Pokémon Emerald (USA/Europe) `.gba` file** (game code `BPEE`). No ROMs are provided or linked.

| Platform | Steps |
|---|---|
| **Android** | Install `gen_3_remake_vX.Y.Z-alpha.apk` from [Releases](../../releases/latest). Allow installs from unknown sources if asked. |
| **Windows / macOS / Linux** | Install [LÖVE 11.5](https://love2d.org), then open `gen_3_remake_demo_vX.Y.Z-alpha.love` with it. |

On first launch, pick your `.gba` file in the launcher. Saves are stored in the app's own save folder and carry
over between versions.

## Modding

Mods are Lua files in the game's `mods/` folder. The engine loads them after its own content, so a mod can add to
or replace anything the built-in quest layer does.

**Install a mod**
- **Android:** share a mod `.zip` to Gen 3 Remake, or copy it into the save folder and tap **IMPORT MOD .ZIP** in the launcher.
- **Desktop:** drag a mod `.zip` or folder onto the game window, or use **IMPORT MOD .ZIP**.
- Each mod has an ON/OFF switch in the launcher's **MODS** panel. Changes apply on the next game start.

**Write a mod**

A mod is a folder with a `mod.lua` inside (single-file mods work too). Here is a complete one that gives the
player three Potions from a Littleroot townsperson:

```lua
-- mods/potion_lady/mod.lua
local Q = api.quest
local FLAG_GAVE = 0x0B0   -- pick an unused flag from pret's FLAG_UNUSED_* list

Q.registerInteract(0, 9, 3, {                    -- LITTLEROOT TOWN, NPC localId 3
    { op = "facePlayer", who = 3 },
    { ["if"] = function() return Q.getFlag(FLAG_GAVE) end, op = "msg", text = "Use it wisely!" },
    { ["if"] = function() return Q.getFlag(FLAG_GAVE) end, op = "jump", to = 99 },
    { op = "msg", text = "You look like you're heading out.\nTake this!" },
    { op = "setFlag", flag = FLAG_GAVE, value = true },
    { op = "giveItem", item = 13, count = 3 },   -- ITEM_POTION
    { op = "msg", text = "Good luck out there." },
})

return { name = "Potion Lady", version = "1.0" }
```

**What the `api` gives you**

| | |
|---|---|
| `api.quest` | NPC talks, map-enter scenes, step triggers, signs, NPC placement/visibility/sprite rules |
| `api.dialogue` | Conditional NPC text tables |
| `api.wild` | Replace any map's grass, water, fishing, or Rock Smash encounters |
| `api.state` | Live game state: player, party, bag, flags, vars, options |

Scripts are lists of commands: `msg`, `move`, `giveItem`, `givePokemon`, `battle`, `choose`, `setFlag`, `setVar`,
`teleport`, `shop`, `heal`, `bgm`, and more. Maps, NPCs, flags, species, and items are addressed with pret's own
numeric ids, so anything you can find in pokeemerald you can use here.

The full reference, more examples, and a worked sample mod (`kanto_welcome`) are on the
[Modding wiki page](../../wiki/home).

## Status

Alpha. The demo is playable start to finish, but expect bugs and some simplified cutscenes. Save often.

Found something? Open an [Issue](../../issues) with what you did, what happened, your platform and version, and a
screenshot if you can.

## Legal

Non-commercial fan project. Not affiliated with or endorsed by Nintendo, Game Freak, Creatures, or The Pokémon
Company. You must own the original game. No ROMs are provided or linked, and no donations are accepted.
See [`LICENSE`](LICENSE) and [`DISCLAIMER`](DISCLAIMER.md).
