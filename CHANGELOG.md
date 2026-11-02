# Changelog

## 0.1.0 (beta)

First release, for **Need for Speed: Underground 2**.

- Blender add-on (Blender 4.2+), sidebar **Cockpit** tab:
  - **Roles** for every moving part: steering wheel, needles (RPM, speed, turbo), rear-view and side mirrors, gear
    lever (keyframed or skinned), handbrake, hanging ornaments, GPS screen, head unit, live texts, player decals,
    hands on the wheel, accessory mounts.
  - **Material kinds** (interior, matte plastic, metal, chrome, car paint, glass, unlit, glow, mirror, GPS);
    textures converted to DXT1 / DXT5 DDS with mipmaps inside Blender.
  - **Check**, with **Fix names**; **Preview** of needles, wheel, lever and handbrake with the game's formulas.
  - **Export to U2** (and install into the game), **Quick test in game** (FRSFastTest, downloaded when the game has
    none; the game boots into the street with the interior on any car and the hood camera; undone when the game
    closes), **Build release zip** for players.
  - **Status** panel: the Cockpit mod and FRSFastTest in the game.
- Example: the Cockpit mod's **Mazda RX-7** interior, set up with the add-on; it exports to the mod's own RX-7 files.
- Help > **Build example cockpit**: a simple interior made from scratch, every role and material kind set up.

Needs a Cockpit mod build with quick-test support for **Quick test in game** (the Status panel tells).
