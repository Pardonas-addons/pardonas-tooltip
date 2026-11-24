# Changelog – Pardona's ToolTips

What changed for players in each version. How everything works is explained in the handbook: https://pardonas-addons.de/tooltips/

## Unreleased

### Added
- New switch **Experimental features** (Automatic / On / Off) in the General section. It turns the features that are still being tested on or off. *Automatic* turns them on in beta versions and off in release versions.
- `/ptt debug` now tells whether you are running a development, beta or release version.

### Changed
- **Pardona** is now the default color set for new installations and after resetting the settings. A color set you chose earlier is kept.
- The spec line, the resource bar and the exact health text are now experimental features: they only appear while the experimental features are on (beta).
- The addon's source code moved to https://github.com/Pardonas-addons/pardonas-tooltip.

## 0.2.0-beta1 – 2026-11-18

### Added
- One shared minimap button for all Pardona addons, with a small menu when several of them are installed.
- Settings group **Pardona's Addons** with an overview page; the ToolTips options are listed below it.
- Launcher "Pardona" for Titan Panel and other LibDataBroker displays.
- `/ptt minimap` shows or hides the shared minimap button.
- Exact health text: current and maximum health on the health bar wherever the game allows it (beta).
- Resource bar for mana, rage, energy and other resources below the health bar (beta).
- Spec line for your own character, estimated from the talent layout (beta).

### Fixed
- Rare mobs are now recognized and marked on the level line.

## 0.1.0-beta1 – 2026-11-16

First beta.

### Added
- Tooltip position, scale, font and font sizes.
- Color sets **Blizzard**, **Dark**, **High contrast** and **Pardona**; optional border color by item quality, class or reaction.
- Players: name and class in class color, guild line color, target (">> YOU <<" when it is you), live movement speed and average item level (other players are inspected out of combat).
- Health percentage on the health bar below the tooltip.
- Mobs: classification (Elite), (Rare), (Rare Elite) or (Boss) on the level line.
- Items: item level in the title line, an always visible gear comparison (Always / Only with Shift / Off) and an option to hide the appearance collection hint.
- Disenchant chances with materials and quantities. With TradeSkillMaster also the disenchant value and a recommendation to sell to a vendor, use the auction house or disenchant, including slow-seller detection.
- Chat commands `/ptt`, `/ptt reset`, `/ptt debug` and `/ptt help`.
- English and German.
