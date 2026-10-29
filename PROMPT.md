# Task: build a Dota 2 Tinker cosmetic set in Blender, "The Polar Sprinter"

You are working on David's personal side project. Build the 3D assets for a Dota 2 Steam Workshop cosmetic set for the hero **Tinker**, using the Blender already installed on this PC. Work only inside `C:\Users\dsing\dota-tinker`. Do not scan or read other folders on this machine. Do not publish, upload or submit anything to Steam, and do not buy anything. No secrets in output.

## The concept
Tinker as an elite cross-country skate sprinter. The look is an homage to a modern Norwegian sprint-champion style: red race suit, wraparound shades, double-poling. Valve will not accept a real athlete's name, face, flag or sponsor logos, so use none of them. A plain bib number "1" is fine.

Palette: red, white and glacier blue, with one warm brass accent. Keep Tinker's goblin-engineer look, with brass rivets under the race panels, so the hero still reads as Tinker at a glance. Avoid pure white and pure black in textures.

## The five pieces
| Slot | Item | Design | LOD0 tris (close-up) | LOD1 tris (in game) | Texture |
|---|---|---|---|---|---|
| Back | Waxroom Belt | Slim race hydration belt with a brass wax iron and a stick of blue glide wax clipped on | 1200 | 500 | 256x256 |
| Head | Glacier Shades | Fitted race headband over Tinker's goggles, mirrored wraparound shades with frosted lenses, small bib clip with a "1" | 3000 | 1200 | 512x512 |
| Weapon | Double-Pole Discharger | Right arm becomes a carbon ski pole with a race basket and grip strap, laser fires from the pole tip as a cold blue beam with ice shards | 3500 | 1400 | 512x512 |
| Offhand | Split-Time Gauntlet | Left arm becomes the matching pole plus a race glove with a stopwatch on the wrist | 3500 | 1400 | 512x512 |
| Shoulders | Bib Number One | The mech body restyled as a red and white aerodynamic race suit with blue piping, a bib plate with a big "1" on the chest, a heart-rate display on the console that glows when Tinker casts. If the feet belong to this slot, they become skate skis with race bindings | 5000 | 3000 | 512x512 |

These limits were read from https://www.dota2.com/workshop/requirements/tinker on 2026-10-16. **Re-fetch that page first and use its current numbers if they differ.** Valve enforces the limits strictly: a file over the limit will not export. The same page links a Tinker model download for previewing items in context. Download it if you can, and use it to fit every piece to Tinker's real proportions. If it needs a login or you cannot get it, say so plainly in STATUS.md and ask David to place it in the project folder. Do not guess the proportions and claim a fit.

## How to work
1. **Read Valve's rules first.** Read the Dota 2 Workshop requirements and item-creation docs (dota2.com/workshop/requirements and the Dota 2 Workshop Tools wiki on developer.valvesoftware.com). Write down what you confirmed: texture types required (color, normal and the mask textures), smoothing rules, naming, and what the Workshop Tools import step expects. Mark anything you could not confirm as **unverified**. Never invent a spec.
2. **Concept art.** Use your image generation tool for front, side and back concept art of the full set on Tinker. Save it in `concept\`. Look at the results and iterate until the set reads clearly. This is reference only, not the final textures.
3. **Prove the pipeline on one piece.** Start with the Back item, the smallest. Find `blender.exe` under `C:\Program Files\Blender Foundation\`. Drive Blender headless with Python scripts you keep in `scripts\`:
   - block out the piece at LOD0
   - make an LOD1 version
   - triangulate a copy and **count triangles programmatically**. Print a table against the limits, and fail loudly if any piece is over.
   - UV unwrap, then paint or bake the textures at the exact sizes above
   - render a turntable or three still angles to `renders\` and look at them
4. **Then build the rest** in this order: Head, Weapon, Offhand, Shoulders.
5. **Export** each piece as FBX to `export\` (LOD0 and LOD1 files), with textures in `export\textures\` using the naming Valve's docs require.
6. **Verify and report.** Write `STATUS.md` with:
   - the triangle count table (actual vs limit) per piece and LOD
   - what is done, and what is not
   - what you confirmed from Valve's docs and what is unverified
   - the exact steps for David to import the files with the Dota 2 Workshop Tools in Steam (the Workshop Tools DLC must be installed from Steam), and whatever is still missing for a real submission

## Rules
- Never claim a piece is done without evidence: the triangle count printed, the renders looked at, and the export files present.
- If something blocks you (the reference model, the Workshop Tools, a spec you cannot confirm), keep going on everything else and list it in STATUS.md.
- Keep the Blender scripts re-runnable, so changing a number and re-running rebuilds the piece.
- Plain, short writing in STATUS.md. No em dashes.
