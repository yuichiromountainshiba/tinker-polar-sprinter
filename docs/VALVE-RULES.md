# Valve rules checked

Checked 2026-10-17. Official pages were fetched before modeling. Local text caches preserve the public Steam Support FAQ body only. No Steam account was used.

## Tinker budgets

| Slot | LOD0 maximum triangles | LOD1 maximum triangles | Texture pixels |
|---|---:|---:|---|
| Back | 1200 | 500 | 256 x 256 |
| Head | 3000 | 1200 | 512 x 512 |
| Weapon | 3500 | 1400 | 512 x 512 |
| Weapon Offhand | 3500 | 1400 | 512 x 512 |
| Shoulders | 5000 | 3000 | 512 x 512 |

These match the brief. The page does not identify a feet slot or state that feet belong to Shoulders. Feet ownership must be checked against the downloaded reference meshes and Item Tools. Do not replace bare hero geometry unless it is part of an item slot.

Source: https://www.dota2.com/workshop/requirements/tinker

Official reference download: https://media.steampowered.com/apps/dota2/workshop/tinker.zip?v=11095536

## Geometry and skeleton

FBX and DMX are supported. SMD is no longer supported. LOD1 is required; LOD0 is optional. Count triangles after triangulation. Valve recommends triangulating before submission to control the result.

Skin each wearable to Valve's supplied default hero skeleton. Preserve names, joint positions, bind pose, and default animations. Do not add bones. Export in the bind pose. Most wearables may use at most 60 existing bones. Do not fit to decompiled game models.

Hard edges and smoothing groups are permitted, but minimize them because they split vertices. Double-sided materials are unsupported; model visible backfaces. Check weights and intersections during attack, cast, idle, run, loadout, and portrait animations, at both LODs.

Valve's FAQ wording about its four-influence limit is ambiguous: it reverses the normal vertex/joint relationship. Conservative implementation is at most four nonzero bone influences per vertex. Exact compiler behavior remains unverified until Item Tools import.

Source: https://help.steampowered.com/en/faqs/view/5FB8-4078-8B2A-C52B

## Textures and masks

Source 2 uses separate texture files for transparency and each shader mask. Packed mask1/mask2 are legacy Source 1 inputs that the importer can convert. New assets should use separate Source 2 maps.

Color may be 24 or 32 bit. Normal must be 24 bit: red left, green down, blue up. Flat normal is RGB 128,128,255. Use exact slot dimensions and equal proportions for every map.

Author color, normal, specular, specular exponent, rimlight, base tint, and self illumination maps. Metalness, detail, and diffuse are enabled only by some hero materials. Tinker-specific availability is unverified. A separate binary transparency map is optional when no cutout is needed. Semi-transparent lenses are not supported by this transparency mask.

All items inherit the hero's default material settings. Custom item shaders and double-sided materials are unsupported. Self illumination is a static brightness mask; it does not by itself implement a cast trigger.

No mandatory source filename suffix scheme was found in the retrieved current docs. Descriptive project suffixes are a local convention, not a verified Valve requirement. Input maps must be assigned to their matching Item Tools fields. Accepted source image extensions and default Tinker material fields remain unverified in the installed importer.

Source: https://help.steampowered.com/en/faqs/view/299C-D7F9-09A5-98B6

## Effects limits

Effects meshes reposition existing Valve ambient particles; they do not author a new ability effect. Where supported, their naming uses an `_fx` postfix. Tinker is not in the documented effects-mesh hero list. No supported cold-blue laser replacement, ice-shard particle system, or cast-triggered heart-rate display was confirmed. Such behavior remains a concept/render treatment until a supported Item Tools path is verified.

Source: https://help.steampowered.com/en/faqs/view/685E-0354-4859-B81F

## Local import and preview

1. In Steam Library, right-click Dota 2. Open Properties and DLC, or View Downloadable Content in older Steam UI. Enable the free Dota 2 Workshop Tools DLC and let it install.
2. Play Dota 2 and choose Launch Dota 2 - Tools. Click Launch Item Tools in the upper section.
3. Click Create New Item. Choose Hero Item, Tinker, and the matching slot.
4. Assign the LOD0 and LOD1 FBX files and individual texture inputs. Keep the default hero skeleton. Fill attachment fields only as the tool requires.
5. Save a separate local workshop session for each piece. Click Next to compile and inspect the Import Log. Fix every reported error.
6. In Preview Model, test animations and Show Low-Res Model. Use Select Wearables to combine the five locally compiled pieces and check existing-item compatibility.
7. Preview in game. Check top-down, loadout, portrait, day/night, attack, cast, idle, and run. Save the session and exit before final upload/submission. Nothing needs to be submitted to perform these previews.

Sources:
- https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Installing_and_Launching_Tools
- https://help.steampowered.com/en/faqs/view/3E00-D38F-B793-7384
- https://help.steampowered.com/en/faqs/view/15B3-1CD0-72CF-A2CF

## Verification limits

The Valve Developer Community Items Overview and installation pages returned HTTP 403 on direct requests. Search indexing exposed the installation instructions, and Steam Support's current item guides provided the import sequence. Item Tools UI labels were not verified on this PC. DLC installation status, current FBX importer compatibility, animated weighting, exact texture fields, feet ownership, particle attachments, and final compiler acceptance still require local Workshop Tools validation.

Entry points:
- https://www.dota2.com/workshop/requirements
- https://www.dota2.com/workshop/
- https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Items_Overview
