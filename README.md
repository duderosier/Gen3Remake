# Gen 3 Remake — Pokémon Emerald on LÖVE2D

A ROM-accurate rebuild of Pokémon Emerald's engine in **Lua / LÖVE2D (LuaJIT)**.
Nothing is redrawn or re-typed: maps, tiles, sprites, dialogue, fonts, music, move/species/item
tables are decoded **live from your own Emerald ROM** every time the game boots.

> **No ROM is included.** You must supply your own legally obtained
> `Pokémon Emerald (USA/Europe)` ROM (game code `BPEE`). The app asks for it on first launch.

## What's in the demo
- Littleroot → Petalburg → Petalburg Woods → Rustboro City (first badge) → Rusturf Tunnel and the Devon Goods, then the demo ends.
- Full battle engine (singles + doubles), abilities, held items, trainer AI, ROM battle animations.
- Wild encounters, fishing, running shoes, item balls, hidden items, Pokémon Center / Mart, PC boxes, Pokédex, Trainer Card.
- Real-time clock and berry growing (Day Care & breeding exist in the engine but sit past the demo's border).
- Touch controls (portrait + landscape), gamepad, keyboard.
- Options: frame style/colour, text speed, battle style — all rendered with the ROM's own window frames and fonts.

## Why
Emerald's behaviour is reproduced from the [pret/pokeemerald](https://github.com/pret/pokeemerald)
decompilation and byte-verified against the ROM. Every flag, var, offset and line of dialogue is checked
before it ships; deliberate deviations are documented.

The engine is built to be **modded like Gen1Recomp**: drop a Lua file in the `mods/` folder and
you can add NPCs, rewrite dialogue, change encounter tables, add quests — no ROM patching, no rebuild.
See **[docs/MODDING.md](docs/MODDING.md)**.

## Install
| Platform | How |
|---|---|
| Android | Install the release APK, launch, pick your ROM file when asked. |
| Windows / macOS / Linux | Install [LÖVE 11.5](https://love2d.org), open `gen_3_remake.love`, pick your ROM. |

Saves and the `mods/` folder live in LÖVE's save directory (path shown in the in-game file picker).

## Controls
| Action | Touch | Keyboard | Pad |
|---|---|---|---|
| Move | D-pad | Arrows / WASD | Left stick / D-pad |
| A / B | A / B buttons | Z / X | A / B |
| Start / Select | Start / Select | Enter / RShift | Start / Back |
| Run | Hold B | Hold X | Hold B |

## Status
Engine is playable to the Mt. Chimney / Lavaridge arc internally; the public demo is capped at Rustboro
to keep it short. Contests, Secret Bases, Battle Frontier and the post-game are not implemented yet.

## Legal
Pokémon and all related names are © Nintendo / Creatures Inc. / GAME FREAK. This is a non-commercial
fan project, distributed **without** any Nintendo assets. Engine code © the author, all rights reserved —
see [LICENSE](LICENSE). Mods you write are yours.
