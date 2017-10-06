#### 1.2.8. Map Sizes (the values provided in the original RMSG are not accurate)
Scaling refers to map area, that is total number of tiles, not side length.
set_scale_by_size and set_scale_by_groups (for terrain and elevation) use a 100x100 = 10000 tiles reference map.
set_scaling_to_map_size (for objects) uses a 100x100 map as a reference. So that is number of objects x area ratio from the table below:


| Size     | Tiles on Sides | Total Tiles | Area ratio to 100x100 map |
|----------|----------------|-------------|---------------------------|
| Tiny     | 120x120        | 14400       | 1.4                       |
| Small    | 144x144        | 20736       | 2.1                       |
| Medium   | 168x168        | 28224       | 2.8                       |
| Large    | 200x200        | 40000       | 4.0                       |
| Huge     | 220x220        | 48400       | 4.8                       |
| Gigantic | 240x240        | 57600       | 5.8                       |
| LudiKRIS | 480x480        | 230400      | 23.0                      |

(LudiKRIS size is only available in The Forgotten and African Kingdoms)
