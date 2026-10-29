# Town Pack — town, home and bar backgrounds with bar ambience

Town Pack is ready-made scenery for a story set in a small town. It supplies three painted backgrounds — a street corner at the town entrance, the vestibule of a house and an evening bar — and the bar's ambient sound loop. It contains no story, scenes or characters: a game decides where the pictures appear.

Two built-in games already share it. **Cthangover** uses the town entrance and the vestibule; the **My Novel** template uses all three backgrounds and the bar ambience. Because both games take the same files from this mod, a fix or an improved picture in Town Pack reaches both.

## What is inside

The town entrance, `town/town_entry`: a cobbled street corner with striped shop awnings.

![The town entrance background: a corner building with green and white awnings on a cobbled street.](assets/town_entry.jpg)

The home vestibule, `home/vestibule`: a hall with a staircase, an armchair and a painting.

![The vestibule background: a wooden staircase, an armchair, a bench and a framed painting in a warm-lit hall.](assets/vestibule.jpg)

The bar, `bar/bar`: tables with lanterns, a counter and shelves of bottles.

![The bar background: lantern-lit tables, a bar counter and shelves of bottles under a beamed ceiling.](assets/bar.jpg)

The bar ambience, `bar/bar_ambient`: an Ogg Vorbis loop of bar atmosphere for the Ambience sound channel.

All three pictures are 1920 × 1024. Each has a grey companion file with the same name and a `_depth` suffix:

![The depth companion of the town entrance: a greyscale version of the same layout.](assets/town_entry_depth.jpg)

You never see a depth picture directly. When a background is shown, the game also loads `<name>_depth` and passes it to the lighting system, which uses it for lights placed over the scene. A background without a depth companion still displays normally.

## Where you see it

- **Cthangover:** the `town_entry` scene (the town entrance) and the `home_vestibule` scene.
- **My Novel template:** `my_novel_town`, `my_novel_home` and `my_novel_bar`. The bar scene also plays `bar/bar_ambient`.

The same town entrance in the My Novel template, where it opens the game with a line of narration:

![My Novel's first scene: the town entrance background behind the line "Evening town. The street lamps are already lit and a cool draught runs along the cobbles."](assets/reuse-my-novel.jpg)

And in Cthangover, where a different story offers its own choices over the same picture:

![Cthangover's town entrance: the same background with the choices "Return home" and "Check the alley".](assets/reuse-cthangover.jpg)

Town Pack is part of both games' collections, so it is loaded with them. Installing it does not add these places to an unrelated game: a game has to use the backgrounds in its own scenes.

## Use the backgrounds in your game

1. Add `town_pack>=1` to your content mod's `depends` list.
2. Add `town_pack>=1` to your game's collection, as the My Novel template does in its **Assets** block.
3. Refer to the resources by their names below. Names are relative to `backgrounds/` and `sounds/` and have no file extension.

```jsonc
// mods/my_game/manifest.json — add to the existing list
"depends": ["town_pack>=1"]
```

A scene that shows the bar and plays its ambience, taken from the template's `my_novel_bar` scene:

```json
{
  "name": "my_bar",
  "defaultBackground": "bar/bar",
  "defaultAmbient": "bar/bar_ambient"
}
```

A scenario can also change the picture during a dialogue:

```scenario
background town/town_entry
text "The street is empty at this hour."
```

The available names are:

```text
town/town_entry     backgrounds/town/town_entry.png
home/vestibule      backgrounds/home/vestibule.png
bar/bar             backgrounds/bar/bar.png
bar/bar_ambient     sounds/bar/bar_ambient.ogg
```

## Replace a picture for your game

To change a picture without editing Town Pack, ship a file with the same relative name, for example `backgrounds/bar/bar.png`, in your own mod and declare `town_pack>=1` in its `depends`. The mod that depends on the owner is loaded later and wins. If you replace a background, also ship a matching `_depth` file with the same name: otherwise Town Pack's original depth picture is still found, and lights follow the old picture's layout.

Without the dependency, two mods offering the same name have no defined order; the resource map tool reports that as an error.

## If something is missing

1. A black or missing background usually means a misspelt name. Names are case-sensitive and use `/`.
2. Check that Town Pack is included in the game you launched, not only installed.
3. No bar sound: check that the scene's `defaultAmbient` is `bar/bar_ambient` and that **Ambience** is enabled in **Settings → Sound**. Sound playback is provided by the Audio Engine mod.
