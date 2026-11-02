# CockpitTools

A Blender add-on for building car interiors for the **Cockpit** mod of the Black Box *Need for Speed* games, by
FRS Mods.

You model the interior in Blender, tell the add-on what each part is (steering wheel, needles, mirrors, gear
lever...) and click **Export to U2**. The add-on writes the files the mod loads, can install them into the game,
start the game straight into the street to test them, and zip them for release.

| File | What it holds |
| --- | --- |
| `COCKPIT_<CAR>.BIN` | the interior's models and textures |
| `COCKPIT_<CAR>.ini` | the rig: driver's eye, steering wheel, needles, mirrors, screens, accessory mounts |
| `COCKPIT_<CAR>_KNOB.BIN` | the gear lever, when it is skinned to two bones (optional) |

## Game compatibility

| Game | Executable | CockpitTools |
| --- | --- | --- |
| Need for Speed: Underground 2 | SPEED2.EXE v1.2 (PC) | **supported**: export, install, quick test, release zip |
| Need for Speed: Underground | speed.exe v1.4 | not yet |
| Need for Speed: Most Wanted | speed.exe v1.3 | not yet |
| Need for Speed: Carbon | NFSC.exe v1.4 | not yet |
| Need for Speed: ProStreet | nfs.exe v1.1 | not yet |

The Cockpit mod itself runs in more of these games; CockpitTools exports for **Underground 2** only for now. The
other games will follow.

## Download

Everything is in one release: the add-on and the example car. Get it from the
[Releases page](https://github.com/chrystianfarias/CockpitTools/releases/latest):

| Asset | Contents |
| --- | --- |
| `CockpitTools-U2-<version>.zip` | **the add-on and the example**, with a README: start here |
| `cockpittools-addon-<version>.zip` | the add-on alone (install it in Blender as it is: do not extract it) |
| `cockpittools-example-rx7-<version>.zip` | the example alone: the mod's Mazda RX-7 interior, with its textures |

## Requirements

- Blender **4.2 or newer** (tested with 5.2).
- To see your interior in the game: NFS Underground 2 with the **Cockpit mod** installed (`scripts\Cockpit.asi`
  and an ASI loader). The quick test needs a Cockpit build that supports it; the add-on's **Status** panel tells.

## Quick start

1. Extract `CockpitTools-U2-<version>.zip`.
2. In Blender: **Edit > Preferences > Add-ons**, the menu at the top right, **Install from Disk...**, pick
   `cockpittools-addon.zip`. Make sure *CockpitTools (NFS Underground 2)* is ticked.
3. In the 3D view press **N** and open the **Cockpit** tab. In the **Car** panel pick your NFSU2 folder (the one
   with `SPEED2.EXE`).
4. Open `Example\EXAMPLE_RX7.blend` (keep its `textures` folder beside it).
5. Click the parts and look at their **Role** in the *Selected object* panel.
6. Click **Quick test in game**: NFSU2 starts in the street with this interior on your car and the hood camera.
   Close the game when you are done; everything is put back as it was.

Then read the [Modeling guide](docs/modeling-guide.md) and make your own.

## Documentation

- [Installation](docs/installation.md) - the add-on, the example, the game folder, the Status panel
- [Modeling guide](docs/modeling-guide.md) - car space, the driver's eye, every part's naming and settings,
  materials and textures, the game's limits
- [Add-on reference](docs/addon-reference.md) - every panel and button
- [Testing and publishing](docs/testing-and-publishing.md) - export, quick test in the game, the release zip
- [Troubleshooting](docs/troubleshooting.md)

## How it works, in one paragraph

The mod's exporter recognises parts by their **object names** (`STEERING_WHEEL`, `POINTER_RPM`, `MIRROR_LEFT`...)
and a few **custom properties** (`u2_gauge_max`, `u2_steering_lock_deg`...). The add-on sets those for you: picking
a role renames the object and gives it its properties, and each material's *kind* becomes the game's light
material and flags at export time, its image converted to a DXT texture. So a `.blend` made with the add-on is a
normal Blender file; you can also name things by hand and the add-on will recognise them.

## Support

If CockpitTools or the Cockpit mod is useful to you, a donation helps keep them going:

**International**

- Buy Me a Coffee: https://buymeacoffee.com/chrystianfarias
- PayPal: https://www.paypal.com/donate/?hosted_button_id=HGV7CJB2DV6EU

**Brasil (PIX)**

- Chave: `adee83c3-dd6d-47a2-ba7a-f5e7a234a78f`
- Nome: Chrystian Farias

## Credits

- **CockpitTools** and the **Cockpit** mod by FRS Mods (Chrystian Farias).
- The example's **Mazda RX-7 interior** comes from *Juiced 2: Hot Import Nights* (Juice Games / THQ).
- The accessories the example mounts by default come with the Cockpit mod, from *Midnight Club: Los Angeles*
  (Rockstar San Diego); they are not part of this release.
- The quick test boots the game with [FRSFastTest](https://github.com/chrystianfarias/FRSFastTest), downloaded from
  its own releases.
- [Blender](https://www.blender.org) by the Blender Foundation.
- *Need for Speed* is a trademark of Electronic Arts; this project is not affiliated with or endorsed by Electronic
  Arts.

## License

Free to use, study, modify and redistribute, with credit to Chrystian Farias and a link back to this repository; it
may not be sold, in whole or in part. Interiors you make with CockpitTools are yours. See [LICENSE](LICENSE) for the
full terms.
