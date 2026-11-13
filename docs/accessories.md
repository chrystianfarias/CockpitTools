# Accessories

Besides whole car interiors, CockpitTools exports **accessories**: parts the players buy in the customization
shop's **INTERIOR** category and fit on any car that has a mount for them (head units, hanging ornaments, gauges,
steering wheels, seats...). One accessory works on every car of the mod, and on yours.

An accessory is two files in `<game>\scripts\Cockpit\Accessories`:

| File | What it holds |
| --- | --- |
| `<ID>.BIN` | its models and textures |
| `<ID>.ini` | its manifest: name, category, price, reputation, its parts (and a hanging ornament's swing) |

The mod lists every `.ini` of that folder in the shop: nothing else to register.

## The examples

The release's `Example-Accessories` folder (or the separate `cockpittools-example-accessories-<version>.zip`) has
one example per category, each set up with CockpitTools (open it and look at the Export panel, the roles and the
material kinds):

| Example | Category | What it shows |
| --- | --- | --- |
| `STEREO_1DIN` | head unit (1-DIN) | the mod's own radio: a faceplate, a display drawn unlit, a live "now playing" text (`TEXT_MUSIC`) |
| `STEREO_2DIN` | head unit (2-DIN) | the mod's double-height unit |
| `LITTLE_TREE` | hanging ornament | the mod's air freshener: one part, `TREE_ATTACH`, hanging from its origin, and its swing |
| `POD_DASH3` | gauge pod | the mod's dash pod with three holes: the empties `HOLE_1`..`HOLE_3` and the hole diameter |
| `TURBO_GAUGE` | gauge | a boost gauge: body, face and its marks, the glow layer, the needle `POINTER_TURBO` and the bracket `BODY_SUPPORT`; colour layers for the shop's gauge colours (`u2_tint`) |
| `MOMO_MILLEN` | steering wheel | a sport wheel, all of it `STEERING_WHEEL` |
| `SEAT_MOMO_RSGT` | seats | a pair of bucket seats, `SEAT_FL` / `SEAT_FR` in car space |
| `NOS_BUTTON` | NOS button | the button on the steering wheel, its cap on the origin |

They are the mod's own accessories: each exports exactly the files the mod ships. Keep each `.blend` with its
`textures` (and `source`) folder. There is no GPS example: the shop's GPS is the mod's own part.

## Setting one up

1. A new file (**File > New > General**), or a copy of an example.
2. Cockpit tab, export panel: **Export: Accessory**, then:

   | Field | |
   | --- | --- |
   | **ID** | its name in the game's files: `<ID>.BIN`, `<ID>.ini`, and the prefix of its parts and textures (upper case letters, digits, `_`; e.g. `FUZZY_DICE`). Players' saves remember it: do not change it after publishing |
   | **Name** | what the shop shows |
   | **Category** | which mounts it fits (below) |
   | **Price**, **Reputation** | its price in the shop, and what it adds to the car's visual rating in the career (500 = one star of 10) |
   | **Swing** (hanging only) | **Length** from where it hangs to its centre of mass (longer = slower swing), **Damping** (how fast the swing dies out), **Twist stiffness** (how hard the string turns it back) |

3. Model it in a collection named **`accessory`** (picking a role puts the object there).
4. **Check**, then **Export to U2**: with **Install in game** ticked, the files go into
   `<game>\scripts\Cockpit\Accessories`. In the game, open the shop's **INTERIOR** on a car with a mount of that
   category and buy it.

The **Quick test in game** is for car interiors; an accessory is tested in the shop. **Build release zip**
(Distribute panel) builds `Cockpit-NFSU2-<ID>-<version>.zip` with `scripts\Cockpit\Accessories\<ID>.*` and a
README for the players.

## Accessory space

The accessory is modelled **in its mount's space**: the origin is the mount's point, and its axes are the mount's,
**X forward** (away from the driver), **Y left**, **Z up**, in metres. In the game it is drawn on the car's
`DUMMY_<MOUNT>` empty: where that empty is, turned as it is.

| Category | Mounts | Where its origin is, how it faces |
| --- | --- | --- |
| **Head unit (1-DIN)** `audio` | `DUMMY_AUDIO` | the radio opening's middle; the faceplate toward the driver (-X), its front 8 mm in front of the origin (X = -0.008), the body behind it (+X). A 1-DIN unit is 178 x 50 mm: the mod scales it to each car's opening (never stretched) and fills round it |
| **Head unit (2-DIN)** `audio2din` | `DUMMY_AUDIO_2DIN` | the same, 178 x 100 mm |
| **Hanging ornament** `hanging` | `DUMMY_HANG` (under the rear-view mirror) | the point it hangs from; it hangs down (-Z). Its part with the **Hanging ornament** role (`<NAME>_ATTACH`, origin = the hanging point) swings with the car |
| **Gauge** `gauge` | `DUMMY_GAUGE<N>`, the pods' holes | the gauge's face toward the driver (-X); its needles are `POINTER_*` (role Needle, as in an interior). The pods fit a gauge by its needle's pivot and its diameter: a bracket under it named `BODY_SUPPORT` is hidden in a pod. A digital gauge without needles marks its centre with an empty `GAUGE_CENTER` |
| **Steering wheel** `steering` | `DUMMY_STEERING` | the wheel's centre on the rim's plane, X along the column; the rim named `STEERING_WHEEL` (role Steering wheel) turns. It hides the car's own wheel |
| **Seats** `seat` | `DUMMY_SEATS` | both seats, as they sit in a car (car space: the driver's on the left, +Y); each car's mount moves them onto its floor. They hide the car's `SEAT_FL` / `SEAT_FR` |
| **GPS** `gps` | `DUMMY_GPS` | the unit on the dashboard, its screen toward the driver (material kind **GPS screen**, UV 0..1 over the screen) |
| **Gauge pod** `gaugepod` | `DUMMY_POD<N>` | the pod's own frame; the car's `DUMMY_GAUGE` children of the mount are its holes |
| **NOS button** `nosbutton` | `DUMMY_NOS_BUTTON` (on the steering wheel) | the button's face toward the driver; it turns with the wheel |

Roles, live texts (`TEXT_MUSIC`, `TEXT_KMH`...) and material kinds work as in an interior (see the
[Modeling guide](modeling-guide.md)), except **Car paint**: an accessory is not painted.

## Names and textures

- Its parts are named `<ID>_<OBJECT>` in the game (27 characters at most); its textures `<ID>_<NAME>` (23 at most):
  a short ID leaves room for the names. **Check** says when one does not fit.
- Images of CockpitTools materials get the ID prefix by themselves. A material with its own `u2_*` properties
  (kind *Manual*, made by another tool) keeps its texture name: **Check** warns when it is not `<ID>` or `<ID>_*`,
  because two accessories (or a car) with a texture of the same name would show each other's.

## Updating one

Export again: the shop reads the files when the game starts. The players keep it fitted as long as the **ID**
stays the same.
