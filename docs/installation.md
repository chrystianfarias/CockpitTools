# Installation

## 0. Download

One release holds everything: open the
[Releases page](https://github.com/chrystianfarias/CockpitTools/releases/latest) and download
`CockpitTools-U2-<version>.zip` (the add-on and the example car). Extract it into a folder of your own:

```
cockpittools-addon.zip      the add-on (do not extract this one)
Example\EXAMPLE_RX7.blend   the example
Example\textures\...
README.txt
```

The same release also has the add-on and the example as separate downloads
(`cockpittools-addon-<version>.zip`, `cockpittools-example-rx7-<version>.zip`), e.g. to update only the add-on.

## 1. The add-on

1. Blender: **Edit > Preferences > Add-ons**. Click the menu at the top right (the small arrow) and pick
   **Install from Disk...**.
2. Select `cockpittools-addon.zip` (or `cockpittools-addon-<version>.zip`). **Do not extract it.**
3. Tick **CockpitTools (NFS Underground 2)** in the list if it is not ticked already.
4. Close the preferences. In the 3D view press **N**: the sidebar shows a **Cockpit** tab.

To update, install the new zip the same way; it replaces the old one. Restart Blender afterwards.

> Blender 4.2+ lists the add-on under *Add-ons* (it is a "legacy" add-on, not an extension: that is expected).

## 2. The game folder

In the **Cockpit** tab, **Car** panel, set **NFSU2 folder** to the game's folder, the one with `SPEED2.EXE`
(and the `scripts` folder). It is stored in the add-on's preferences, so you set it once for every `.blend`.

## 3. The Status panel

Right below the Export panel, **Status** tells whether the game is ready for the add-on:

| Line | Meaning |
| --- | --- |
| *Cockpit mod: installed (supports the quick test)* | all good |
| *Cockpit mod: installed, but too old for the quick test* | export works, the quick test does not: update the mod |
| *Cockpit mod: installed, but no ASI loader* | the mods will not load: put an ASI loader (`dinput8.dll`) beside `SPEED2.EXE` |
| *Cockpit mod: not installed in this game* | install the Cockpit mod first |
| *FRSFastTest: the game's own (...)* | the game already has FRSFastTest (or FRSFastBoot): the quick test uses it, with its settings |
| *FRSFastTest: downloaded (...)* | the add-on downloaded it; it is copied into the game only while a test runs |
| *FRSFastTest: not downloaded yet* | the first quick test downloads it from GitHub; or click **Download FRSFastTest** now |

[FRSFastTest](https://github.com/chrystianfarias/FRSFastTest) is what makes the game boot straight into the street.
You never need to install it yourself.

## 4. The example

The example is in the release's `Example` folder (or the separate `cockpittools-example-rx7-<version>.zip`):

```
Example\EXAMPLE_RX7.blend
Example\textures\...        the interior's textures (the .blend points at them: keep them together)
```

Open `EXAMPLE_RX7.blend`. It is the Mazda RX-7 interior the Cockpit mod ships, set up with CockpitTools: steering
wheel, needles, the three mirrors, a skinned gear lever, the GPS screen and accessory mounts. Exporting it gives
exactly the files of the mod's RX-7.

Accessories have examples of their own, in the release's `Example-Accessories` folder (or the separate
`cockpittools-example-accessories-<version>.zip`): one per category (head units, hanging ornament, gauge pod, gauge,
steering wheel, seats, NOS button). See [Accessories](accessories.md).

Prefer a smaller start? **Help > Build example cockpit** builds, in an empty file (**File > New > General**), a
simple interior made from boxes, with every role and every material kind set up.
