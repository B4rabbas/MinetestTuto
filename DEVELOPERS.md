Here is some useful info for developers.

### How the map is saved
The map is not stored in a traditional way, like in real Minetest world. Instead, the tutorial generates the world on-the-fly when the player creates a new world.

The tutorial castle is saved in the game itself in schematics and other binary metadata files in `mods/tutorial/mapdata`. When you start a new world, Tutorial force-sets the mapgen to `singlenode`, loads the schematics and places them. After that, it generates the grassland surroundings.

## How to edit the map
### Mod security
First, you need to list `tutorial` as a trusted mod because the `/tsave` command needs write access.
You can review the relevant code in `mods/tutorial/mapgen.lua`.

### Editing the map
You want to only edit the map data files. Here's how:

In `minetest.conf`, add the following settings:

```
tutorial_debug_map_editing = true
tutorial_debug_edit_item_spawners = true
```

This enables the `/treset` and `/tsave` commands to help editing the schematic. It also forces the Tutorial to only generate the raw castle, not the grasslands. Also, the item spawners become visible.

Create a new world in Creative Mode. Now edit the map to your likings using your instant digging power and the creative inventory. You can of course WorldEdit to speed up the process.
If you're finished, use the `/tsave` command. This updates the map files in `mods/tutorial/mapdata`. Note that there are limits as for how big the tutorial castle can be.

### About item spawners
To place items in the map, you must use the item spawners, these are simple nodes that spawn items. They have 2 states: active and inactive.

Inactive basically means "unconfigured". An inactive item spawner is made when you place one from the creative inventory. Place it somewhere where you want the item. If that place would be water, place it somewhere nearby. Rightclick the node and enter the itemstring and an optional offset. The item will spawn at the node position plus the offset. Click OK to make the item spawner active. You can't edit an item spawner once its configured, just remove it and place a new one.

In the finished map, all item spawners must be configured and active.

If you mess with item spawners, the setting `tutorial_debug_edit_item_spawners` MUST be `true` before you load the map.

### Testing and finalizing
To test your new map, remove the 2 `minetest.conf` settings and create a new world and check if everything works. If it does work, you can commit your changes now.

(Note: The `/tsave` command is not available if the `tutorial` mod failed to request an "insecure" environment due to mod security issues.)
