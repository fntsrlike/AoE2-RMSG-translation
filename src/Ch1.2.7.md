#### 1.2.7. <OBJECTS_GENERATION>
物件（Objects）包括單位（unit）、建築（buildings）、資源（resources）和一些類似老鷹的裝飾。

##### Commands
```
create_object TYPE  { ... }
```
為玩家或大地之母建立一或多個指定型別的物件。
警告：作者曾經因為使用超過 99 個 `create_object` 指令導致遊戲崩潰。

##### Attributes
```
number_of_objects N
```
要放置幾個。預設值為 `1`。

```
number_of_groups N
```
建立幾個群組，每個群組都會擁有數個 `number_of_objects` 所指定的值。也就是說，物件總數為 `number_of_objects X number_of_groups`。預設沒有群組：物體是獨立的，完全分散。

```
group_variance N
```
只有在搭配 `number_of_groups` 時會運作：將給麽群組的物件是賦予一個隨機誤差值。他會將原本 `number_of_objects` 加上一個隨機產生介於 -N ~ N 的值。（例如，一個透過 `number_of_objects 5` c和 `group_variance 2` 產生的鹿群，可能會有 3 到 7 隻鹿，也就是 5 ± 2 隻。
- 每個群組會有不同的是數量。
- 群組至少會有一單位的物件。

```
set_scaling_to_map_size  /  set_scaling_to_player_number
```
擇一使用。調整群組的數量：如果未定義 `number_of_groups` ，則會調整 `number_of_objects`。
- `set_scaling_to_map_size`：未調整的數值將參照 100x100 的地圖。
- `set_scaling_to_player_number`： 所有群組數量 = `number_of_groups` * `number of players`。
（這個屬性只會影響數量，不要跟 `set_place_for_every_player` 搞混了！）

```
set_place_for_every_player
```
將物件作為每個玩家的私有物件，像是初始的村民。對於非玩家的物件也有作用，例如每個人初始地附近的私人金礦（但需要搭配 `set_gaia_object_only`。

- 就算你沒辦法建造或生產的建築、單位，你也可以放置。例如，就算在黑暗時代或是美洲文明的情況下，你仍可以放置馬廄，只是無法生產任何騎兵類單位。
- 只有在玩家土地有被定義時才會有作用。
- 你無法將單位放置在那些已經被水或是不可放置單位的地形從遊戲者所有土地隔離出去的土地上。
- 通常來說，這個屬性對置水上單位是沒有作用的，所以你不可以放置初始船隻、碼頭等等，除了：
    * 當玩家土地是由泥土 (DIRT, DIRT2, DIRT3, DIRT_SNOW) 組成時。
    * 對電腦遊戲者有作用。
    * 當水是玩家土地的一部分時。
    * 無法在 land_id 被使用時有作用。

作者表示，儘管擁有許多實驗，但他仍然找不到邏輯所在。

```
set_gaia_object_only
```
讓物件屬於非玩家（大地之母）。一般來說，所有物件在沒有設置 `set_place_for_every_player` 屬性時，都屬於大地之母的。

- 對於不可控制的物件，如果有設置 `set_place_for_every_player` 時，就必須搭配本屬性。
- 如果你是使用可控的物件（單位建築），並且讓他成為中立的（可被救援的）。物件會在第一個玩家經過時，擁有屬於他，但不是用電腦遊戲者。

```
terrain_to_place_on TYPE
```
物件只會被放置在這個屬性指定的地形中。正常來說，多數的通用物件會被放置在有理可循的地形（像是於不會放在陸地上、遺跡不會在水上、黃金不會在道路上⋯⋯等等。），總之，你無法將物件放置在奇怪的地形上。
但是有些裝飾物件可能會被放置在奇怪的地形上，這時候你就可以使用本屬性去避免這種情況。

```
min_distance_to_players N,  max_distance_to_players N
```
距離玩家土地中心的最小與最大距離。你可以只使用其中一個，或是兩個屬性都使用。
一般來說是沒有距離限制。然後城鎮中心是使用 `max_distance_to_players 0` 讓他位在土地中心。

- 當有使用 `set_place_for_every_player` 時，距離只會以各自的遊戲者為主。
- 當沒有宣告 `set_place_for_every_player` 時，`max_distance_to_players` 是沒作用的，而 `min_distance_to_players` 則是確保能與**所有土地**的中心保持最小距離。如果你有不少非玩家土地，這個屬性可以限制物件的放置。
- 如果有使用 `place_on_specific_land_id` ，距離會以該土地中心為為止。
- 如果有定義 `number_of_groups`，
If number_of_groups is defined, distance refers to centers of groups.
If these distance limits are very strict (e.g. min = max), objects tend to appear mostly on the left.

```
max_distance_to_other_zones N
```
Minimum (NOT maximum!!) distance in tiles from borders of zones; useful to keep objects away from shores.
If number_of_groups is defined, distance refers to centers of groups.

```
min_distance_group_placement N
```
Scatters objects, keeping them at least N tiles away from any other object of any type.
Keeps away only objects created by the same create_object command, or placed later; does not work for objects placed earlier. To be sure that two series of objects aren't close, add this attribute to both creation statements.
If number_of_groups is defined, distance applies among centers of groups, not among objects of same group.
WARNING: This attribute will affect ALL objects placed after this command. If you want to scatter objects created in the same create_object command without restricting future object placement, it is best to use temp_min_distance_group_placement to do so. Use min_distance_group_placement with smaller values to prevent objects created in future commands from ending up directly next to the current ones.  Both attributes can be used together in the same create_object command.  Inappropriate use of min_distance_group_placement may result in objects towards the end of your script not being placed at all!

```
temp_min_distance_group_placement N
```
Scatters objects created by current create_object command, keeping them at least N tiles away from each other.
If number_of_groups is defined, distance applies among centers of groups, not among objects of same group. Only used for relics in the standard maps; however is often a good idea to use this attribute for any objects that need to be scattered far apart from each other (like wolves, or extra map resources).

```
group_placement_radius N
```
Force objects in every group to stay within N tiles from center of group. Default is 3 tiles (7x7 square area).
- `group_placement_radius` overrides other attributes, including `number_of_objects`. For large groups, you need a large `group_placement_radius`; by default, groups can contain no more than 7x7=49 objects

```
set_tight_grouping  /  set_loose_grouping
```
Use one or other. Tight groups have no space among objects (like gold and stone in standard maps).
Loose groups can have 1 or 2 tiles among objects; set_loose_grouping is default and can be omitted.
- `set_tight_grouping` doesn't place objects that are larger than 1 tile and can't overlap (like most buildings)

```
place_on_specific_land_id N
```
Places objects only on the Land marked by land_id N.
-      Does not work with personal objects (with set_place_for_every_player)
-      Land must be separated from others by water (or shallow / ice / beach for objects not allowed there)
-      If there are multiple lands with the same id, the set number of objects is placed on each of them

```
resource_delta -N
```
Modify the resources of a specific instance of an object. (only works with UP, not in the HD Edition)
This allows you to, for example, produce a gold mine with only 300 gold in it.  Does not work in the scenario editor.
