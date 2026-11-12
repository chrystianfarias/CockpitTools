# Modeling guide

Everything the Cockpit mod reads comes from the `.blend`: the parts' **names**, a few **custom properties**,
the **materials** and the **driver's eye** camera. The add-on sets all of it from its panels; this page says what
each part is and how it must be built, so the result works in the game the first time.

- [Car space and the scene](#car-space-and-the-scene)
- [The driver's eye](#the-drivers-eye)
- [Static parts](#static-parts)
- [Parts table](#parts-table)
- [Steering wheel and hands](#steering-wheel-and-hands)
- [Needles](#needles)
- [Mirrors](#mirrors)
- [Gear lever](#gear-lever)
- [Handbrake](#handbrake)
- [Hanging ornaments](#hanging-ornaments)
- [GPS screen](#gps-screen)
- [Head unit (HTML screens)](#head-unit-html-screens)
- [Live texts](#live-texts)
- [Player decals](#player-decals)
- [Wipers](#wipers)
- [Accessory mounts](#accessory-mounts)
- [Materials](#materials)
- [Textures](#textures)
- [The game's limits](#the-games-limits)
- [Tips](#tips)

## Car space and the scene

- **Units and axes:** metres; **X forward, Y left, Z up**. The origin is the origin of the game's car model, so the
  interior must sit where the car's cabin is. The example RX-7 (and the mod's other cars) is a good ruler: the
  driver's eye is around `(-0.07, 0.38, 1.06)`, left-hand drive (the driver at **+Y**).
- **What is exported:** the objects in the collection **`interior`** (its child collections too). Anything else is
  ignored, so reference models, the car's body, lights... can stay in the file outside it.
- **The car:** the **Car** panel's name is the game's car *type* name (`350Z`, `PEUGOT`, `SKYLINE`, `RX7`...; the
  field lists them as you type). The interior appears on that car only.
- **The driver:** the mod draws its own driver (arms, hands on the wheel, the right hand to the gear knob). You do not
  model one. Leave room for the arms between the seat and the wheel.

## The driver's eye

A **camera** marked as the driver's eye: select it, *Selected object* panel, **Driver's eye** (or **Help > Add driver
camera**, which makes one at the 3D cursor looking forward).

| What | How |
| --- | --- |
| Position | the eye, in car space |
| Direction | the camera looks down its local **-Z**; its local **Y** is up (a camera rotated `90, 0, -90` looks along +X) |
| Field of view | the **horizontal** one (*Sensor Fit: Horizontal*, which the button sets); 75° is a good start |
| Near plane | *Clip Start*: 0.15 m or more (closer planes make the game flicker) |

The camera may be outside the `interior` collection. Players can still move the eye and change the field of view in
their own settings; your camera is the starting point.

## Static parts

Any mesh in `interior` that has no role is a **static part**: dashboard, seats, doors, pillars, roof... It is drawn
where it is in the `.blend`, with its modifiers applied.

- **Names:** plain ASCII (letters, digits, `_`, `.`, `-`), short: a part's name in the game is the car's prefix plus
  the object's name, **27 characters** at most (see [limits](#the-games-limits)). **Check** flags names that do not
  fit and **Fix names** shortens them.
- An object whose materials mix lit kinds with unlit ones (*Unlit*, *Glow*, *GPS screen*) becomes two parts in the
  game, `<NAME>` and `<NAME>_U`: that is automatic.
- Faces need a material each, and a UV map if the material has a texture.

## Parts table

Pick the role in **Selected object > Role**; the object is renamed for you. The names below are what the mod reads,
so you may also type them yourself.

| Role | Object | Name | Moves |
| --- | --- | --- | --- |
| Static part | mesh | any | no |
| Steering wheel | mesh | `STEERING_WHEEL` (its glow layer: `STEERING_WHEEL_GLOW`) | turns with the steering |
| Needle | mesh | `POINTER_<X>` + `u2_gauge_*` properties | turns with RPM, speed or boost |
| Rear-view mirror | mesh | `MIRROR_CENTER` | shows the game's rear view |
| Left / right mirror | mesh | `MIRROR_LEFT` / `MIRROR_RIGHT` | own cameras |
| Gear lever | mesh | `GEAR_SHIFT_KNOB` (keyframed), or a skinned lever | follows the gear |
| Handbrake | mesh | `HANDBRAKE` (keyframed) | follows the handbrake |
| Hanging ornament | mesh | `<NAME>_ATTACH` | swings |
| GPS screen | mesh | `SCREEN_GPS` (or a material named `GPS`) | shows the minimap |
| Head unit | mesh | `MULTIMIDIA` (also `SCREEN_WEB*`, `SCREEN_<X>`) | an HTML page |
| Live text | text | `TEXT_<SOURCE>` | speed, RPM, gear, music |
| Player decals | mesh | `DECAL_<REGION>` | shows the player's decals |
| Wiper | mesh | `WIPER_<X>` | sweeps the windscreen, clearing the rain |
| Hands on the wheel | empty | `GRIP_L` / `GRIP_R` | - |
| Accessory mount | empty | `DUMMY_<MOUNT>` | - |

A name repeated with Blender's `.001` suffix (`STEERING_WHEEL.001`) is no longer recognised and becomes a static part;
**Check** warns about it.

## Steering wheel and hands

- **Name:** `STEERING_WHEEL`. Everything that turns with the wheel (spokes, horn pad, buttons) must be in that one
  object; a second object named `STEERING_WHEEL_GLOW` turns with it too (lit buttons). Other objects, even parented
  to the wheel, do not turn.
- **Origin:** the wheel's centre, on the column's axis.
- **Axis:** the wheel turns about its **local X**, along the column (pointing forward, away from the driver, as the
  example's). Rotate the object so its local X runs down the column; apply scale, keep the rotation.
- **Settings:**

  | Setting | Property | Default |
  | --- | --- | --- |
  | Turn at full lock (degrees) | `u2_steering_lock_deg` | 270 |
  | Direction | `u2_steering_sign` (1 / -1) | set from the axis when the role is picked |

  Check the direction in **Preview**: *Steering* **+1 must turn the wheel to the left**. If it turns right, press
  **Flip**. Note: the mod's player setting `SteeringLockDeg` (in `Cockpit.ini`, 160 by default) takes precedence over
  your lock angle; yours is used when a player sets it to 0.
- **Hands:** two empties, `GRIP_L` and `GRIP_R`, at the driver's wrists on the rim; their axes are the hands' axes.
  They may be parented to the wheel. Without them the mod uses its default grip, made for a wheel like the
  example's.

## Needles

- **Name:** `POINTER_<X>`, with the role's quantity:

  | Quantity | Property value | Default range |
  | --- | --- | --- |
  | Rev counter | `engine_rpm` | 0 - 8000 |
  | Speedometer | `speed_mph` (miles per hour, also for km/h dials: set the max to the dial's top in mph) | 0 - 160 |
  | Turbo | `turbo_boost` (the HUD's boost gauge, spread over min..max) | -1 - 2 |

- **Origin:** the needle's pivot (the dial's centre).
- **Axis:** the needle turns about its **local Z**, which must point **at the driver** (out of the dial's face).
- **Pose:** the `.blend`'s pose shows the **minimum** value (or the value in *Value the pose shows*,
  `u2_gauge_rest`, if you modelled it elsewhere).
- **Settings:** *Minimum value* `u2_gauge_min`, *Maximum value* `u2_gauge_max`, *Sweep to the maximum (degrees)*
  `u2_gauge_sweep_deg`: the angle from the pose to the maximum. **Negative = clockwise** as the driver sees it (the
  usual), positive = counter-clockwise; **Flip** swaps it. A 270° dial from 7:30 to 4:30 is `-270`.
- **Material:** usually *Unlit* (needles stay readable at night).
- Check it in **Preview** (*RPM*, *Speed*, *Turbo* sliders).

## Mirrors

| Mirror | Name | What it shows |
| --- | --- | --- |
| Rear-view | `MIRROR_CENTER` | the game's own rear-view mirror image |
| Side mirrors | `MIRROR_LEFT`, `MIRROR_RIGHT` | an image from a camera of its own, the driver's eye reflected in the glass |

Rules for all three:

- The object is **the glass only**: one flat face (or a few coplanar faces) facing the driver, its housing a separate
  static part.
- **UV 0..1 over the whole glass**, U to the driver's right as seen from the seat. (Side mirrors are flipped by the
  export, as a mirror is: do not flip them yourself.)
- Turn the glass **halfway between the driver's eye and straight back**: that is what a real mirror shows.
- The rear-view mirror's material: kind *Rear-view mirror* (automatic when the object is a mirror).
- Make sure nothing hides them from the eye: side mirrors are seen through the side windows, so keep the window
  sills below them. They are outside the straight-ahead view (players look with the mouse), as in a real car.

## Gear lever

Two ways; the mod's driver moves his right hand to the knob on a gear change with either.

**Keyframed** (simplest): name the lever `GEAR_SHIFT_KNOB`, origin at its pivot (the boot), and record one pose per
frame with the pose buttons in *Selected object* (position it, press the red button):

| Frame | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Gear | N | 1 | 2 | 3 | 4 | 5 | 6 | R |

The lever goes through neutral only across the gate (2-3, 4-5, 1-R), as an H pattern does.

**Skinned** (the example's; the knob bends instead of turning whole): an **armature with two bones** deforming the
lever mesh:

- a bone named **`Bone`**: the lever. Its **head is the pivot**, its **tail is where the hand holds the knob**;
- a second bone (any name, e.g. `Root`): what stays still (the boot);
- the mesh weight-painted to both (the lever's vertex group named `Bone`), with an Armature modifier pointing at the
  armature. The add-on recognises such a rig by itself, whatever the armature and the mesh are called.

The export then writes `COCKPIT_<CAR>_KNOB.BIN`, which the mod draws in place of the mesh.

## Handbrake

Name `HANDBRAKE`, origin at its pivot; **frame 0 released, frame 1 pulled** (the pose buttons again).

## Hanging ornaments

An air freshener, a charm...: any mesh whose name ends with **`_ATTACH`**. Its **origin is the point it hangs
from**; the `.blend`'s pose is its rest. It swings with the car's motion (players tune the physics). A thin card
works best; it is lit from above on both faces.

## GPS screen

An object named `SCREEN_GPS` (or any object with a material named `GPS`, or of the kind *GPS screen*): the game's
minimap is drawn there. **UV 0..1 over the screen**, the screen's top at V = 1.

## Head unit (HTML screens)

An object named `MULTIMIDIA` shows an HTML page, drawn by the mod's *CockpitWeb* (players need it installed; without
it the screen shows its splash or black). **UV 0..1 over the screen** = the page's viewport. By default it shows the
mod's shared head unit (`carplay`). Optional properties (custom properties on the object):

| Property | Meaning | Default |
| --- | --- | --- |
| `u2_web_page` | the page, relative to the mod's `Cockpit\Web\pages` (`bin:<file>` = a page of your own, see below) | `carplay/index.html` |
| `u2_web_size` | the page's size, `WxH` | 1024 wide, height from the screen's shape |
| `u2_web_transparent` | the page's background shows through | off |
| `u2_web_interactive` | the player can click it with the zoomed aim | on for `MULTIMIDIA` |
| `u2_web_splash` | a picture shown until the page loads | `splash.png` in the web folder |

**Pages of your own:** put them in a folder named `web` beside the `.blend`; they are packed into the `.BIN` and the
screen opens `bin:index.html`. Other screens open the page named after them in lower case: `SCREEN_CLOCK` opens
`bin:screen_clock.html`.

## Live texts

A Blender **Text** object named `TEXT_<SOURCE>`; the mod writes the live value in its place:

| Source | Shows |
| --- | --- |
| `KMH` / `MPH` | the speed |
| `RPM` | the engine's revs |
| `GEAR` | the gear (`R`, `N`, `1`...) |
| `MUSIC` | the song playing (scrolls) |

- The text's **number of characters** is the display's size: type `000` for a 3-digit speedometer.
- Its **alignment** (Text properties > Alignment) and its **colour** (the material's Emission colour, or Base Color)
  are used.
- Place and size it as it should look; the game draws it on a flat quad over the text's box.

## Player decals

A mesh named `DECAL_<REGION>` shows the stickers the player put on that region of the car, seen from inside (e.g. a
sun strip on the windscreen). Its material must be one of the game's decal slots, **`DUMMY_DECAL1` ... `DUMMY_DECAL8`**
(name the material so), mapped like the car's own decal geometry. Regions: `HOOD`, `FRONT_WINDOW`, `REAR_WINDOW`,
`LEFT_DOOR`, `RIGHT_DOOR`, `LEFT_QUARTER`, `RIGHT_QUARTER`.

## Wipers

`WIPER_<X>`, origin at the pivot, at rest. The export turns each wiper's frame so its local Z is the windscreen's
normal (the windscreen: the object `GLASS_FRONT`, or any `*GLASS_FRONT*`) and measures the rubber's reach (a material
named `RUBBER` or `BLACK`, else the outer part of the blade). In the game the wipers sweep the glass (the player's K
key) and clear the rain where they pass. Only in the exported files: your `.blend` is not changed.

## Rain on the glass

Nothing to do: every object with a *Glass* material gets, in the export, a rain layer over its glass, and
`COCKPIT_<CAR>.glass` maps each window for the drops (up to 16 windows). Name the windscreen `GLASS_FRONT` so the
wipers and the drops know which glass is the windscreen.

## Accessory mounts

Players can fit accessories sold by the mod (gauges, gauge pods, steering wheels, head units, a GPS, ornaments, seats,
a NOS button) on your interior.
You only place **mounts**: empties named **`DUMMY_<MOUNT>`**. The mount's **origin and axes are the accessory's**
(X forward, Y left, Z up when the empty is not rotated).

| Mount name starts with | Category | Hides the car's part while an accessory is fitted |
| --- | --- | --- |
| `DUMMY_GAUGE` | gauge | - |
| `DUMMY_STEERING`, `DUMMY_WHEEL` | steering wheel | `STEERING_WHEEL` (and `_GLOW`) |
| `DUMMY_AUDIO`, `DUMMY_RADIO`, `DUMMY_STEREO`, `DUMMY_DVD` | head unit | - |
| `DUMMY_HANG` | hanging ornament (keep the empty upright: it hangs along -Z) | - |
| `DUMMY_SEAT` | seats (the pair) | `SEAT_FL`, `SEAT_FR` |
| `DUMMY_GPS` | GPS (the mod's GPS unit; not fitted by default) | - |
| `DUMMY_POD` | gauge pod (a dash or A-pillar pod with 1-3 holes) | - |
| `DUMMY_NOS_BUTTON` | NOS button (make it a child of `STEERING_WHEEL`: it turns with the wheel) | - |

Optional properties: `u2_mount_category` (overrides the name), `u2_accessory` (the accessory fitted by default, e.g.
`LITTLE_TREE`), `u2_mount_hides` (the car's parts hidden while one is fitted, comma separated). In the game the player
buys and fits them in the customization shop's **INTERIOR** category (the camera moves into the car).

Without a seat mount, the export adds `DUMMY_SEATS` at the car's origin (the seat accessories are made in car space).

### Gauge pods

A gauge pod is a mount like the others (`DUMMY_POD1`, `DUMMY_POD2`...: role *Mount: Gauge pod*): place it where the
pod sits, its axes the pod's. Its holes are **`DUMMY_GAUGE<N>` empties parented to it**, one per hole, each where the
gauge's face goes (Z toward the driver): the export fits each gauge to its hole. The holes show in the shop only
while a pod is fitted on that mount; a `DUMMY_GAUGE` that is not a pod's child is a gauge slot of the car itself
(always there).

## Materials

Build materials as usual: a **Principled BSDF** with an **Image Texture** in *Base Color*. Then pick each material's
**kind** in the *Selected object* panel (or leave *Auto*, which guesses from the name and use):

| Kind | For | In the game |
| --- | --- | --- |
| Interior | dashboard, seats, doors, trim | the texture lit by the car's light |
| Matte plastic | dark plastic, rubber, carpet | duller |
| Metal / aluminium | brushed metal, pedals | with reflections |
| Chrome | chrome trim | strong reflections |
| Car paint | parts in the body colour (door tops, the dash of some cars) | **the colour the player picked**; your texture is not used |
| Glass | windscreen, windows | the mod's light glass seen from inside; **normals must face outward** |
| Unlit (always lit) | needles, dial faces, screens | not affected by light or shadow |
| Glow (lit overlay) | lit dials and buttons, as a layer over the base | always lit; **black = no glow**; the image in *Emission Color* (else *Base Color*) |
| Rear-view mirror | the rear-view mirror's glass | the game's mirror image |
| GPS screen | the GPS screen | the minimap |
| Manual (u2_*) | materials made by another converter | left as they are (see below) |

**Transparency** (Interior, plastic, metal, chrome, unlit): *Auto* uses the texture's alpha when the Principled
BSDF's *Alpha* is linked (or below 1); force it with *Use the texture's alpha* / *Opaque*. Transparent textures are
DXT5, opaque ones DXT1.

**Glowing dials:** the dial face as *Interior*, plus a copy of its faces a millimetre in front with a *Glow* material
whose image is the lit markings on black. The example does this.

**Manual materials** (advanced): a material with the custom properties `u2_texture`, `u2_light_material`, `u2_flags`
(hex string), `u2_shipped`, `u2_unlit`, `u2_blend` is exported as it is, its texture read from
`textures\<u2_texture>.dds` beside the `.blend`. The RX-7 example uses these.

## Textures

- Use any image Blender reads (PNG, JPG, TGA, EXR...), packed or on disk. No image: the material's colour becomes a
  small solid texture.
- At export, each image becomes a DDS in a **`textures`** folder beside the `.blend` (converted again only when the
  image changes): resized to a power of two, at most the **Max texture** size of the Car panel (1024 by default),
  with mipmaps.
- Texture names in the game are the car's prefix plus the image's name, cut to 23 characters: give images short,
  distinct names (`dash.png`, `seat.png`...).
- Optional: a colour attribute named **`Color`** on a mesh darkens it per vertex (baked ambient occlusion).

## The game's limits

| Limit | Value | What happens |
| --- | --- | --- |
| Vertices per object | 65535 (after splitting at UV seams and hard edges) | export error: split the object |
| Part name | 27 characters, with the car's prefix (`<CAR>_INT_` for short car names, `<CAR>_` for long ones) | **Check** error; **Fix names** |
| Texture name | 23 characters, with the prefix | cut automatically |
| Characters in names | ASCII | **Check** error; **Fix names** |

## Tips

- **Mid tones.** The mod lights the cabin softly. Textures that look dark grey in Blender look black in the game;
  aim for 30-60% brightness and put detail in them (grain, stitching, vents).
- **Scale applied, rotation kept.** Apply scale (Ctrl+A) on moving parts; their rotation defines their axes.
- **Watch the eye.** Look through the driver's camera (Numpad 0) while you model: that is the only view players get.
- **Check often.** **Check** catches most mistakes before the game does.
- **Test in the game.** **Quick test in game** takes about a minute; see
  [Testing and publishing](testing-and-publishing.md).
