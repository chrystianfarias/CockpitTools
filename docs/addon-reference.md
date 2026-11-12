# Add-on reference

Everything is in the 3D view's sidebar (**N**), **Cockpit** tab, in this order.

## Cockpit U2 - Car

| Item | What it does |
| --- | --- |
| **Car** | the game's car type name the interior is for (`350Z`, `PEUGOT`, `RX7`...). The field lists the 31 cars as you type; the car's full name shows below it |
| **Prefix** | the prefix of every part and texture name in the pack. Empty = automatic (`<CAR>_INT_`, or `<CAR>_` for long car names). Change it only if two interiors of yours clash |
| **Max texture** | the largest texture size in the pack: 256 / 512 / 1024 / 2048 |
| **Output folder** | where the files are written; `//cockpit_export` = a folder beside the `.blend` |
| **NFSU2 folder** | the game's folder (with `SPEED2.EXE`). Kept in the add-on's preferences, for every file |
| **Install in game** | after **Export to U2**, copy the files into `<game>\scripts\Cockpit` |
| **Check** | lists what would stop the export or come out wrong in the game: errors (red) and warnings. The arrow button beside a line selects the object |
| **Export to U2** | checks, converts the textures, writes `COCKPIT_<CAR>.BIN` / `.ini` / `.glass` (and `_KNOB.BIN`), and installs them when ticked |
| **Quick test in game** | exports and starts the game with this interior; see [Testing and publishing](testing-and-publishing.md). While the game runs the button says *Test running: close the game* |
| **Open folder** | opens the output folder |
| **Fix names** | appears when **Check** finds names the game cannot take: renames those static parts (upper case, ASCII, short enough) |

The list under the buttons shows the last **Check** or export: errors, warnings, the files written and installed.

## Status

| Line | |
| --- | --- |
| *CockpitTools add-on: installed* | the version you run |
| *Cockpit mod: ...* | whether the mod is in the game, supports the quick test, and has an ASI loader |
| *FRSFastTest: ...* | the game's own, downloaded by the add-on, or not yet |
| **Download FRSFastTest** | shown until it is downloaded: gets it now instead of on the first test |

See [Installation](installation.md#3-the-status-panel) for what each state means.

## Selected object

The active object's name, then:

- **Role** menu: what the object is (the list depends on the object's type: mesh, empty, text, camera). Picking a role
  renames the object and gives it its settings; picking *Static part* (or *None*) gives it its old name back. A role
  that only one object may have (the steering wheel, the mirrors...) is refused while another object has it.
- the role's description, and its **settings**:

| Role | Settings |
| --- | --- |
| Needle | *Minimum value*, *Maximum value*, *Sweep to the maximum (degrees)* with **Flip**, the direction (clockwise / counter-clockwise), *Value the pose shows* |
| Steering wheel | *Turn at full lock (degrees)*, *Direction* with **Flip** |
| Gear lever | the pose buttons N, 1-6, R |
| Handbrake | the pose buttons *Released*, *Pulled* |
| Head unit | *Page* (or **Own page...**) |
| Accessory mount | the category, *Default accessory* (or **Accessory fitted by default...**) |
| Live text | the characters count, *Alignment*, the colour's source |
| Camera | **Driver's eye**, *Field of view (horizontal)*, *Near plane* |

**Pose buttons** (gear lever, handbrake): the label goes to the pose's frame (to see or adjust it); the red button
records the object's current location and rotation as that pose.

**Material** box (for the active material of a mesh):

| Item | |
| --- | --- |
| **Kind** | the material's role in the game; *Auto* shows what it guessed. See [Materials](modeling-guide.md#materials) |
| **Alpha** | transparency for the kinds that can have it: *Auto*, *Use the texture's alpha*, *Opaque* |
| Texture | the image the texture is made from, or *No texture: solid colour* |
| In the game | after an export: the texture's and the light material's names in the pack |

## Distribute

The release zip's details: **Name**, **Author**, **Version**, **Description** (one line), **Preview picture**
(PNG/JPG, optional). The zip's name shows below; **Build release zip** exports and writes it into the output folder.
See [Testing and publishing](testing-and-publishing.md#the-release-zip).

## Preview

Tick the panel's header to preview, in the viewport, what moves in the game, with the game's own formulas:

| Control | Moves |
| --- | --- |
| *RPM*, *Speed*, *Turbo* (0..1 of each needle's range) | the needles |
| *Steering* (-1 full right .. +1 full left) | the steering wheel |
| *Gear* N, 1-6, R | the gear lever (keyframed) |
| *Handbrake pulled* | the handbrake |

The preview never changes your poses (it uses the objects' delta rotation and the timeline), and it switches off on
export and when the file is opened. **Turn it off before editing the parts.**

## Help

| Button | |
| --- | --- |
| **Quick guide** | opens the guide (`COCKPIT_GUIDE`) in a Text Editor area (open one first to read it there) |
| **Build example cockpit** | in an empty scene: builds a simple interior with every role and material kind |
| **Add driver camera** | adds the driver's eye camera at the 3D cursor, looking forward |

## Without Blender's interface

The add-on's folder has `headless.py`, for scripts and batch jobs:

```
blender -b MyCar.blend --python <add-on folder>/headless.py -- export [--car 350Z] [--out DIR] [--game DIR] [--no-install]
blender -b MyCar.blend --python <add-on folder>/headless.py -- test --game "C:\Games\NFSU2"
blender -b MyCar.blend --python <add-on folder>/headless.py -- dist
```

`<add-on folder>` is where Blender installed it, e.g.
`%APPDATA%\Blender Foundation\Blender\5.2\scripts\addons\cockpittools`.
