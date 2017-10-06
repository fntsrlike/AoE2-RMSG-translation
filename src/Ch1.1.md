<!--
世紀帝國 II 系列：《隨機地圖腳本指南》CH1.1: 腳本參考範本
AOE II: RMSG CH1.1 - Scheme of a RMS
-->

本文件譯自 [Bultro] 和 [Zetnus] 所編寫的[《Updated New RMS Guide (v2.0.0)》][Guide]，並取得作者同意以標示名稱為翻譯授權。

[Guide]: http://aok.heavengames.com/cgi-bin/forums/display.cgi?action=ct&f=28,42485,0,365
[Bultro]: http://aok.heavengames.com/blacksmith/showprofile.php?author=Bultro
[Zetnus]: http://steamcommunity.com/id/zetnus

本文章主要提供一個腳本的參考範本，讓開發者藉此對之前與接下來的說明有更明確的概念。

## 正文

本節提供腳本的骨架（skeleton），之中有許多可能會用到的指令與其所需的參數，讓想要建立新腳本的開發者，能從這參考範本複製所需要的指令、貼到自己的腳本中。詳細請待我慢慢詳述。

- `N` 代表自然數，可能會是一個範圍。小數和負數是不被允許的。
- `%` 代表百分比 (0-100)。小數點是不允許的。不需要再輸入 ％。
- `TYPE` 代表一個標識常數，像是 `GRASS`。型別（type）會在「地形與物件」的章節詳述。如果你輸入一個不合法（不存在的型別），那什麼事情都不會發生。
- `/` 代表你需要在多個屬性中選擇其中一個，請不要把所有屬性都填進去。
- `[UP/HD]` 代表這個命令只支援 [User Patch] 和 [HD] 版本的世紀帝國，原版未包含此命令。實際使用時，請將這個註記刪除。

<!--more-->

```text
<PLAYER_SETUP>
random_placement / grouped_by_team[UP/HD]
nomad_resources[UP/HD]

<LAND_GENERATION>
base_terrain TYPE

create_player_lands
{
    terrain_type TYPE
    land_percent % / number_of_tiles N
    base_size N
    base_elevation[UP/HD] N(1-7)
    left_border %, right_border %, top_border %, bottom_border %
    border_fuzziness %
    clumping_factor %
    zone N / set_zone_randomly / set_zone_by_team
    other_zone_avoidance_distance N
}

create_land
{
    terrain_type  TYPE
    land_percent % / number_of_tiles N
    base_size N
    base_elevation[UP/HD] N(1-7)
    left_border %, right_border %, top_border %, bottom_border %
    land_position %(0-100) %(0-99)
    border_fuzziness %
    clumping_factor %
    zone N / set_zone_randomly
    other_zone_avoidance_distance N
    land_id N
    assign_to_player N(1-8)
}

<ELEVATION_GENERATION>
create_elevation  N(1-7)
{
    base_terrain TYPE
    number_of_tiles N
    number_of_clumps N
    set_scale_by_size
    set_scale_by_groups
    spacing N
}

<CLIFF_GENERATION>
min_number_of_cliffs N
max_number_of_cliffs N
min_length_of_cliff N
max_length_of_cliff N
cliff_curliness %
min_distance_cliffs N
min_terrain_distance N

<TERRAIN_GENERATION>
create_terrain TYPE
{
    base_terrain TYPE
    land_percent % / number_of_tiles N
    number_of_clumps N
    set_scale_by_size
    set_scale_by_groups
    spacing_to_other_terrain_types N
    set_avoid_player_start_areas
    height_limits N(0-7) N(0-7)
    set_flat_terrain_only
    clumping_factor %
}

<CONNECTION_GENERATION>
create_connect_all_players_land / create_connect_teams_lands /
create_connect_all_lands / create_connect_same_land_zones
{
    default_terrain_replacement TYPE
    replace_terrain TYPE TYPE
    terrain_cost TYPE N(1-15)
    terrain_size TYPE N N
}

<OBJECTS_GENERATION>
create_object TYPE
{
    number_of_objects N
    number_of_groups N
    group_variance N
    set_scaling_to_map_size / set_scaling_to_player_number
    set_place_for_every_player
    set_gaia_object_only
    terrain_to_place_on TYPE
    min_distance_to_players N, max_distance_to_players N
    max_distance_to_other_zones N
    min_distance_group_placement N
    temp_min_distance_group_placement N
    group_placement_radius N
    set_tight_grouping / set_loose_grouping
    place_on_specific_land_id N
    resource_delta[UP] -N
}
```

## 開發輔助

在編寫腳本時，最痛苦的就是沒有程式碼上色以及語法提示。因為本站目前是使用 highlihght.js 作為程式碼上色的工具，但之中並沒有包含 RMS腳本的上色規格，所以本站無法提供一個閱讀起來最舒適程式碼給讀者。建議在閱讀這份範本，或是自己想要編寫看看時，可以使用 Visual Studio Code 並搭配擴充套件 [AoE2 Random Map Scripting]，如此只要是以 `.rms` 為副檔名的檔案，都會有程式碼上色作為開發輔助。

[![][VS-Code-RMS-Extension]][VS-Code-RMS-Extension]
**圖 2-1**：Visual Studio Code 擴充套件：AoE2 Random Map Scripting

[![][VS-Code-Syntax-highlight]][VS-Code-Syntax-highlight]
**圖 2-2**：RMS 程式碼上色演示

[User Patch]: http://userpatch.aiscripters.net
[HD]: http://store.steampowered.com/app/221380/Age_of_Empires_II_HD/
[AoE2 Random Map Scripting]: https://marketplace.visualstudio.com/items?itemName=deltaidea.aoe2-rms
[VS-Code-RMS-Extension]: https://blog.fntsr.tw/wp-content/uploads/2017/09/VS-Code-RMS-Extension-Demo.png
[VS-Code-Syntax-highlight]: https://blog.fntsr.tw/wp-content/uploads/2017/09/VS-Code-Syntax-Highlight-Demo.png

