# Pardona's ToolTips

A tooltip addon for **World of Warcraft: Forever** (Interface 16001, Mainline client with the Midnight API).

> **Beta** – this addon is in an early stage. The current version covers the tooltip appearance, player and mob information (including spec), item level, gear comparison and disenchant/price information. Please report problems in the GitHub issues.

**Changelog:** [CHANGELOG.md](CHANGELOG.md) · https://pardonas-addons.de/tooltips/changelog

## Features (current state)

### Appearance

- **Position** for tooltips with the default anchor (for example units in the world):
  mouse cursor (default, follows the mouse with a small offset), top left, top right,
  bottom left, bottom right, screen center, or Blizzard default (unchanged).
  The corner positions use an adjustable edge distance (0–200 px, default 20).
  Tooltips of bag slots and buttons keep their usual place.
- **Scale** from 50 % to 200 % (steps of 5 %), applied to the tooltip and the comparison tooltips.
- **Font**: Friz Quadrata, Arial Narrow, Skurri or Morpheus. If another addon provides
  LibSharedMedia-3.0, its fonts are offered as well (the library is not included).
  Separate font sizes for the header line and the text; small lines are drawn two points
  smaller than the text.
- **Color sets** for background, background opacity, border and the colors of the
  addon's own lines:
  - *Blizzard* – the standard look
  - *Dark* – almost black background (about 90 %), thin gray border
  - *High contrast* – black background, white border, strong text colors
  - *Pardona* – deep night blue with a subtle golden border (default for new installations
    and after *Reset settings*; a color set you chose earlier is kept)
- **Color border** (on by default): items in their quality color, players in their class
  color, NPCs in their reaction color (hostile, neutral, friendly).

### Players and mobs

Blizzard's lines are kept. Existing lines are only recolored; the addon's own lines are
added at the bottom. If the unit under the mouse is also your target, its values are read
through your target, which the game often reveals in more detail.

- **Players**: name in class color, guild line in the guild color of the color set, class
  name in class color.
- **Mobs**: classification on the level line. If the game already writes it there (for
  example `Elite`), that word is only colored; otherwise *(Elite)*, *(Rare)*,
  *(Rare Elite)* or *(Boss)* is appended. Normal mobs get nothing. With the option off the
  level line stays unchanged. The word is recognized in the spelling of the game's own
  strings and in the addon's own spelling (`Rare`, German `Rar`); for rare mobs also the
  item quality word (`Rare`, German `Selten`), because this client has no own string for it.
- **Health text** on the health bar below the tooltip, for example `79%`; if the percentage
  cannot be read either, the text is left out.
  - *Exact health text (beta):* with the experimental features on, the text shows current
    and maximum health, for example `812 / 1,025 (79%)` (number format follows the client
    language). WoW Forever hides the current health from addons, even your own, but lets the
    addon pass it on for display; the maximum is readable. The text is therefore shown in full
    whenever possible, otherwise only the percentage.
- **Target** of the unit in class or reaction color, or `>> YOU <<` if it targets you.
- **Speed**: current movement speed in percent of normal run speed, updated live while the
  tooltip shows the unit.
- **Resource bar** (beta, only with the experimental features on): a second bar directly below the health bar, same width and height, in
  the color the game uses for the resource (mana blue, rage red, energy yellow …; blue if
  unknown), with the same text as the health bar, for example `1,815 / 1,863 (97%)`. Like the
  health bar it hangs below the tooltip and never covers its lines. It follows the unit's
  resource live while the tooltip shows it. Units without a resource (maximum 0) or whose
  maximum is hidden get no bar. Works for players and mobs.
- **Item level** (players): average item level with one decimal. Your own character is
  calculated directly. Other players are inspected only out of combat, only when they can
  be inspected and are in range, at most one request every 1.5 seconds; results are kept
  for 10 minutes. If the result arrives while the tooltip still shows that player, the line
  is added. Inspect requests of other addons are not disturbed.
  The average covers the equipped slots except shirt and tabard (17 slots including the
  ranged slot); a two-handed weapon with an empty off-hand counts twice.
- **Spec** (players; beta, only with the experimental features on): the talent tree with the most points and the points of all trees, for
  example `Spec: Arms (31/20/0)`; on a tie both names, for example `Arms/Fury (20/20/11)`.
  No line without spent points. Your own character is read directly, other players with the
  same inspect request as the item level (same rules and cache). The line needs the game's
  talent tree functions; if the client does not offer them, it is not shown (`/ptt debug`
  tells whether they are available).
  - *Experimental, own character only:* WoW Forever names the three trees but reports no
    spent points. The addon then reads the talents of your active talent configuration and
    counts the points per tree by position: it assumes the three trees are drawn side by
    side, left to right in tab order, equally wide. If that assumption is wrong for a class,
    the numbers are wrong too. Other players get no spec line until a reliable way is found.

### Experimental features

Features marked *beta* are still being tested and depend on the switch *Experimental
features* (options, section *General*):

| Feature | When the experimental features are off |
| --- | --- |
| Spec line (players) | no spec line |
| Resource bar | no resource bar (and no replacement line) |
| Exact health text (`current / max (percent)`) | percentage only, for example `79%` |

- *Automatic* (default): **on** in beta and development versions (version contains `beta` or
  `alpha`, or a development checkout), **off** in release versions.
- *On* / *Off*: set by hand, regardless of the version.
- The change applies to the next tooltip, without `/reload`. The tooltip of the switch shows
  the detected version type and what *Automatic* means for it; `/ptt debug` prints the
  detected build type, the setting and the effective value.
- The single options of these features (*Health text*, *Resource*, *Spec*) carry the mark
  *(experimental)*; they only take effect while the experimental features are on.

### Items

- **Item level** of equipment (weapons, armor, jewelry, shields, off-hand items), shown
  right-aligned in the title line as `iLvl 25`. If that place is already used, an own line
  `Item level: 25` is added instead. Consumables, materials, recipes and quest items get no
  item level. Works in the normal tooltip, chat link tooltips and Blizzard's comparison
  tooltips.
- **Always visible gear comparison** below the tooltip (normal tooltip and chat links) for
  equipment your character can wear (the character level is ignored). The numbers come from
  the same game function Blizzard uses for its "If you replace this item" section, so they
  match Blizzard's Shift comparison; stat names are the game's own, localized texts.
  - One block per equipped item: `Instead of <item>:` followed by the changed values
    (`+7 Armor` as gain, `-3 Stamina` as loss), or `no change`.
  - Rings and trinkets: one block for each equipped ring or trinket.
  - One-hand weapons: against the main hand, plus the off-hand if you can dual wield.
  - Two-hand weapons: one block against main and off-hand together.
  - Shields and off-hand items: against the off-hand, or against an equipped two-hand weapon.
  - Empty slot: `(empty slot)` with all values of the new item as gains.
  - No comparison for the item you are wearing and in the comparison tooltips.
  - Blizzard's own Shift comparison is not changed.
- **Hide the appearance collection hint** ("You haven't collected this appearance"); the line
  is removed before it is drawn, without leaving a gap.
- Lines of other addons (for example TradeSkillMaster or ArkInventory) are not changed.

### Prices and disenchanting

For disenchantable items – uncommon (green), rare (blue) and epic (purple) weapons and armor –
a block above the comparison shows:

- **Disenchant**: possible materials with chance and quantity, for example
  `75% Soul Dust (1–2) · 20% Greater Astral Essence (1–2) · 5% Large Glimmering Shard`.
  Long lists wrap onto indented lines. If you know Enchanting but your skill is too low,
  `(Enchanting 150 required)` is added. Material names come from the game in your language.
- **Disenchant value** (needs TradeSkillMaster): TSM's price source `Destroy`.
- **Recommendation** (needs TradeSkillMaster): *Vendor*, *Auction house* or *Disenchant*,
  whichever earns the most, for example `Recommendation: Disenchant (≈ 11s 52c)`.
  - Vendor: TSM `VendorSell` (or the game's sell price).
  - Auction house: TSM `DBMarket` (or `DBMinBuyout`) minus the auction house fee. Items with a
    low region sale rate (`DBRegionSaleRate`) or few sales per day (`DBRegionSoldPerDay`)
    count as slow sellers; their auction value is ignored and `(AH: slow seller)` is shown.
    Both figures are read with their decimals (for example a sale rate of 0.737), the same
    values TSM shows in its own tooltip.
  - Disenchant: TSM `Destroy` minus the auction house fee; only counted if you can disenchant
    the item yourself (Enchanting learned and skill high enough) or the item is not bound
    (you can send it to an alt).

When the block is shown: items that are not soulbound always get it; soulbound items only if
your character has learned Enchanting. Chat links and vendor items count as not bound unless
they bind when picked up.

The disenchanting table (Classic item levels) was built from the public tables on
[warcraft.wiki.gg: Disenchanting tables](https://warcraft.wiki.gg/wiki/Disenchanting_tables)
and [warcraft.wiki.gg: Disenchanting](https://warcraft.wiki.gg/wiki/Disenchanting)
(required skill), see `Data/Disenchant.lua`.

### General

- All changes take effect immediately, without `/reload`.
- English and German.

The addon respects the "secret values" of the Midnight API: values that the game hides from
addons are never compared or shown. A line whose values are hidden is simply left out, and
in combat or restricted content no inspect requests are made.

## Installation

1. Download the latest release from GitHub (or CurseForge, once available).
2. Extract the `PardonasToolTips` folder into
   `World of Warcraft\_forever_\Interface\AddOns\`.
3. Restart the game or type `/reload`.

## Optional addons

Pardona's ToolTips works on its own. These addons add features when they are installed:

| Addon | Adds |
| --- | --- |
| TradeSkillMaster | Prices, disenchant value and the sell recommendation |
| AtlasLoot Forever | Needed for the full item source feature (dungeon and raid boss loot, planned) |

Without them everything else works; only these parts are missing. The addon does not
include or change them, it only reads TradeSkillMaster's public API.

## Pardona's Addons

Pardona's ToolTips shares one entry point with the other Pardona addons (for example
Pardona's Buff Reminder) through the embedded library lib-pardona:

- **One minimap button** for all Pardona addons. It can be dragged along the minimap edge;
  its position and visibility are shared by all Pardona addons and kept after `/reload`.
  - Only ToolTips installed: left-click opens the ToolTips options directly.
  - Several Pardona addons installed: left-click opens a small menu with one row per addon
    and "Pardona settings"; right-click opens the overview.
  - The tooltip of the button shows every addon with its status. ToolTips shows *active*,
    or *active (no TSM)* when TradeSkillMaster is not loaded.
- **Settings category "Pardona's Addons"** with an overview page (all Pardona addons, their
  status and a *Show minimap button* checkbox) and the ToolTips page below it.
- **Addon compartment** entry "Pardona's Addons" (if the client has the compartment).
- **Titan Panel and other LibDataBroker displays:** a launcher "Pardona" with the addon
  statuses as text. It only appears if LibDataBroker is already loaded by another addon
  (for example Titan Panel); LibDataBroker is not included.
- `/ptt minimap` or the *Show minimap button* option shows or hides the shared button. Hide
  it there if you prefer the panel launcher.

The library must lie at exactly `Libs\lib-pardona` inside the addon folder: the Pardona
emblem textures are loaded from there, and the overview shows the version from the TOC
(`dev` in a development checkout).

If the library is missing (for example a development checkout without `Libs/`), everything
works as before: the options are a category of their own, there is no minimap button, and
`/ptt minimap` only says that the shared library is not loaded.

## Slash commands

| Command | Description |
| --- | --- |
| `/ptt` or `/pardonastooltips` | Open the options |
| `/ptt reset` | Reset all settings to their defaults |
| `/ptt debug` | Show what the game lets the addon read (see Troubleshooting) |
| `/ptt minimap` | Show or hide the shared Pardona minimap button (needs lib-pardona, see Pardona's Addons) |
| `/ptt help` | List the commands |

If `/ptt` is used during combat, the options open as soon as combat ends.

## Troubleshooting

If something is missing (for example the health text or the resource bar of another player), type
`/ptt debug`. The addon then prints to the chat what the game lets it read, for your character,
your mouseover unit, your target and – in a group – the first party member:

- whether the unit exists, its name and whether its GUID is readable (for the mouseover
  unit also whether it is the same unit as your target),
- health and maximum health, and the health percentage,
- the resource type with its name, current and maximum value, and the resource percentage,
- whether the game's functions for hidden values (`issecretvalue`, `C_Secrets`, percent
  functions) exist, and the `C_Secrets` checks for units,
- whether the talent tree functions exist and your own spec,
- the talent block: every value of `GetTalentTabInfo` per tree (type and value), the active
  talent configuration, its tree IDs, the number of talent nodes, the range of their
  positions, the sum of purchased ranks and the number of nodes with a rank,
- which game events the addon skipped because this client does not know them.
- the build type (`dev`, `beta` or `release`), the experimental setting and its effective value,
- the raw text of every left line of the tooltip currently shown (`secret` for hidden lines;
  color codes are printed, not applied) – useful to see how the game writes a mob's level
  line, for example on a rare mob,

Every value is shown as it is, as `secret` (the game hides it from addons) or as `nil`
(no value). Hover a unit with the mouse and type the command into the chat to include it.
Please add this output when you report a problem.

## Options

Open with `/ptt`, via the Pardona minimap button or via *Options → AddOns → Pardona's Addons → ToolTips*.
Without the shared library (see Pardona's Addons) the page is *Options → AddOns → Pardona's ToolTips*, as before.

**Appearance**

| Option | Default |
| --- | --- |
| Position | Mouse cursor |
| Edge distance (corners only) | 20 px |
| Scale | 100 % |
| Font | Friz Quadrata |
| Font size: header | 14 |
| Font size: text | 12 |
| Color set | Pardona (new installations and after a reset; earlier choices are kept) |
| Color border | On |

**Players & Mobs** (each can be switched off on its own)

| Option | Default |
| --- | --- |
| Name in class color | On |
| Guild color | On |
| Color class line | On |
| Health text (experimental: exact text) | On |
| Target | On |
| Speed | On |
| Resource (mana, rage, energy …) – resource bar (experimental) | On |
| Item level (players) | On |
| Spec (players) (experimental) | On |
| Classification (mobs) | On |

**Items**

| Option | Default |
| --- | --- |
| Item level on items | On |
| Show comparison | Always (choices: Always, Only with Shift, Off) |
| Hide appearance collection hint | On |

With *Only with Shift* the comparison appears and disappears as soon as Shift is pressed or
released.

**Prices & Disenchanting**

| Option | Default |
| --- | --- |
| Show disenchant chances | On |
| Show disenchant value | On |
| Show recommendation | On |
| Auction house fee | 5 % (0–20) |
| Slow seller: minimum sale rate | 0.10 (0.00–1.00) |
| Slow seller: minimum sold per day | 0.5 (0–20) |

If TradeSkillMaster is not loaded, the section says so; prices and the recommendation are
then disabled, the disenchant chances still work.

**General**

- *Experimental features* – Automatic (on in beta versions), On or Off; default Automatic
  (see Experimental features).
- *Show minimap button* – shows or hides the shared Pardona minimap button (On; only with the
  shared library). The setting applies to all Pardona addons and is not changed by *Reset settings*.
- *Reset settings* – restores all defaults.

## Planned

- Item sources (dungeon and raid boss loot with AtlasLoot Forever)
- Vendors and recipes

## Libraries

Embedded when the addon is packaged (`.pkgmeta` externals, folder `Libs/lib-pardona`); they
are not part of this repository:

| Library | License |
| --- | --- |
| [lib-pardona](https://github.com/Pardonas-addons/lib-pardona) (LibPardona-1.0) | MIT |
| LibStub (shipped with lib-pardona) | Public Domain |

For development, `tools\fetch-libs.ps1` copies the library into `Libs\lib-pardona` – from a
sibling checkout `..\lib-pardona` if there is one, otherwise with `git clone --depth 1`.
It can be run again at any time and replaces the folder completely.

## License

Pardona's ToolTips is released under the [GNU General Public License v3.0](LICENSE).
