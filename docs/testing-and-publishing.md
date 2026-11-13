# Testing and publishing

## Export

**Export to U2** (Export panel) runs **Check** first and stops on errors. Then it:

1. converts the materials' images to DDS in `textures\` beside the `.blend` (only the ones that changed);
2. writes into the output folder (`cockpit_export` beside the `.blend` by default):
   - `COCKPIT_<CAR>.BIN` - models and textures
   - `COCKPIT_<CAR>.ini` - the rig (do not edit it by hand: the next export rewrites it)
   - `COCKPIT_<CAR>.glass` - the rain on each window (when the interior has glass)
   - `COCKPIT_<CAR>_KNOB.BIN` - only with a skinned gear lever
3. with **Install in game** ticked, copies them into `<game>\scripts\Cockpit`.

In the game, pick the car and the **hood camera**. If the game is open, the copy fails (*in use*): close it and
export again.

## Quick test in the game

**Quick test in game** shows your interior in the game in about a minute, without touching your game setup:

1. It exports, and copies the files into the game as **`COCKPIT_CTTEST.*`** - a name of its own, so an interior you
   have installed under the car's real name is never overwritten.
2. It writes `scripts\Cockpit\CockpitTools-Test.ini`, which tells the Cockpit mod to show that interior **on
   whatever car you drive** and to start with the **hood camera**.
3. It makes the game boot straight into the street with **FRSFastTest**:
   - if the game already has FRSFastTest (or its old name, FRSFastBoot), it is used as it is, with its settings
     (e.g. your career and your car);
   - otherwise the add-on downloads the latest release from
     [github.com/chrystianfarias/FRSFastTest](https://github.com/chrystianfarias/FRSFastTest) (once; kept in
     `%LOCALAPPDATA%\CockpitTools`) and copies it into the game for this test only, in *dev* mode: straight into the
     city, no save needed.
4. It starts `SPEED2.EXE`.

**Close the game to end the test.** The add-on then removes the test file, the `COCKPIT_CTTEST.*` files and the
temporary FRSFastTest. If Blender was closed before the game, the next export or test cleans up.

Requirements (the **Status** panel shows them): the Cockpit mod installed, in a build that knows the quick test, and
an ASI loader. If the game is already running, the test refuses to start.

What to check in the game:

- the eye's position and field of view (compare with the mod's other cars);
- the steering wheel turns the right way and the hands sit on the rim;
- the needles move and rest where they should;
- the mirrors show an image (look left and right with the mouse for the side mirrors);
- glass, glow and transparency look right at day and at night.

## The release zip

1. Fill in the **Distribute** panel: **Name** (e.g. *Toyota Supra interior*), **Author**, **Version**,
   **Description**, and optionally a **Preview picture** (a screenshot of the interior in the game).
2. Click **Build release zip**. It exports and writes `Cockpit-NFSU2-<CAR>-<version>.zip` into the output folder:

```
scripts\Cockpit\COCKPIT_<CAR>.BIN
scripts\Cockpit\COCKPIT_<CAR>.ini
scripts\Cockpit\COCKPIT_<CAR>.glass        (the rain on the windows)
scripts\Cockpit\COCKPIT_<CAR>_KNOB.BIN     (with a skinned gear lever)
README.txt                                  for the players: what it is, how to install and uninstall
preview.png / .jpg                          when you picked one
```

Players extract the `scripts` folder into the game folder (the one with `SPEED2.EXE`); they need the Cockpit mod.

**Accessory mounts** in your interior work with the accessories that come with the mod; the zip does not carry
accessories.
