# Changelog

## 0.2.2 (beta)

For the Cockpit mod 0.2.2 (NFS Underground 2): CockpitTools now follows the mod's version numbers.

- **Export to U2** works with the mod's 0.2.2 exporter (0.1.0's add-on stopped with a missing module).
- **Accessory mounts**: *Gauge pod* (`DUMMY_POD`, its `DUMMY_GAUGE` children are its holes, shown in the shop only
  while a pod is fitted) and *NOS button* (`DUMMY_NOS_BUTTON`, on the steering wheel); the accessories are bought in
  the shop's INTERIOR category.
- **Rain on the glass**: every window gets its rain layer and `COCKPIT_<CAR>.glass`, installed and zipped with the
  rest; the drops run on the glass and the wipers clear them, as in the mod's own cars.
- **Wipers** (`WIPER_<X>`): turned about the windscreen's normal and given their rubber's reach in the export, so
  they sweep the glass in the game. Your `.blend` is left as it was.
- **Seats**: a `DUMMY_SEATS` mount is added in the export when the interior has none (the mod's seat accessories).
- Help > **Build example cockpit**: its windscreen is `GLASS_FRONT` (the rain and the wipers find it by that name).
- The RX-7 example exports exactly as the mod's own RX-7 (pack, rig, gear lever and rain map).

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
