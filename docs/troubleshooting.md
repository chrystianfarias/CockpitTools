# Troubleshooting

## In Blender

| Problem | Fix |
| --- | --- |
| No **Cockpit** tab | press **N** in the 3D view; check the add-on is ticked in **Edit > Preferences > Add-ons** |
| *save the .blend before exporting* | the textures are written beside the `.blend`: save it once |
| *missing collection "interior"* | put the interior in a collection named `interior` (child collections are fine) |
| *no camera marked as the driver's eye* | select the camera > **Driver's eye**, or **Help > Add driver camera** |
| *... has faces without a material* | give every face a material (empty material slots count as none) |
| *... needs a UV map* | mirrors and screens need UV 0..1 over the surface |
| *name too long, or with accents/spaces, for the game* | **Fix names**, or rename the object by hand (ASCII, short) |
| *... more than 65535 vertices* (export) | split the object (Edit Mode > P > By Material / Selection) |
| *image ... was not found* | **File > External Data > Find Missing Files**, or pack the images |
| *... needs keyframes (0 = rest, one per pose)* | record the gear lever's / handbrake's poses with the pose buttons |
| *there is already an object STEERING_WHEEL* | only one object may have that role: give the other one another role first |
| A part disappeared from the export | is it in the `interior` collection? Is its name a role name with `.001`? |
| The interior looks black in the game | the textures are too dark: aim for 30-60% brightness |
| Preview moved my parts | it never changes the pose: switch Preview off (panel header). Saved while previewing? Opening the file resets it |

## In the game

| Problem | Fix |
| --- | --- |
| No interior at all | the hood camera? the right car? Read `scripts\Cockpit.log`: it says which interiors it loaded, or why not |
| *not installed: ... in use* | the game was open during the export: close it and export again |
| The quick test opens the menus | the game's own FRSFastTest/FRSFastBoot is disabled (`Enabled=0` in its ini), or the mod is too old (Status panel) |
| The steering wheel turns the wrong way | select it > **Flip**; check in **Preview** that +1 turns it left |
| A needle turns the wrong way, or too far | **Flip** its sweep; check the minimum, maximum and sweep; the pose must show the minimum |
| A side mirror is black or missing | the glass must be flat with UV 0..1, facing the driver, and visible from the eye (not behind the door or a pillar) |
| The rear-view mirror shows a frozen picture | the hood camera was switched on late in an old build; restart the test, or switch the camera once (C) |
| The glass is dark or invisible | its material kind must be *Glass* and its normals must face **outward** |
| The driver's hands float | add `GRIP_L` / `GRIP_R` empties on the rim |

## Still stuck?

Open an issue with: the Blender version, the add-on's version (Status panel), what **Check** says, and the game's
`scripts\Cockpit.log`.
