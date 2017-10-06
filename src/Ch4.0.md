## 4. EXAMPLE SCRIPT
This is a short, commented example of a working RMS. The map is very simple, just an example, not worth playing. I’ve rearranged it to reflect the order in which the map components are actually generated.

```

/* ***** Example RMS: Relic isle ***** */
start_random
    percent_chance 50
        #define SUMMER  /* 50% chance of being a "summer" map */
    percent_chance 50
        #define WINTER  /* 50% chance of being a "winter" map */
end_random

if SUMMER  /* define different items for every season */
    #const GROUND 0  /* grass */
    #const WOODS 10  /* oak forest */
    #const TREE 349  /* oak */
else
    #const GROUND 32 /* snow */
    #const WOODS 21  /* snowy forest */
    #const TREE 413  /* snowy pine */
endif  /* this is more practical than doubling and if-ing every create command! */

<PLAYER_SETUP>
random_placement
/* you have to type this... don't ask me why */
/* Actually, you don’t have to type this because random_placement happens by default */

<LAND_GENERATION>
base_terrain WATER

create_player_lands
{
    terrain_type GROUND  /* grass or snow, as defined above */
    land_percent 60  /* 60% is quite high, but will be divided among players */
    base_size 10  /* player lands are wide enough */
    zone 1  /* all player lands are zone 1, they can touch each other */
    other_zone_avoidance_distance 5  /* but stay 5 tiles away from zone 2 */
}

create_land  /* the "relic isle" :) */
{
    terrain_type GROUND
    number_of_tiles 1000  /* fixed size */
    left_border 30  right_border 30  /* keep this isle near the center of the map */
    top_border 30  bottom_border 30
    clumping_factor 15  /* roundish */
    zone 2
    other_zone_avoidance_distance 5
    land_id 111
}

<ELEVATION_GENERATION>
create_elevation 5
{
    base_terrain GROUND
    number_of_tiles 1000
    number_of_clumps 10  /* about 100 tiles per hill */
    set_scale_by_size  /* both total size and number of hills scale with map */
    set_scale_by_groups  /* so bigger maps have more hills, of same size */
}

<CLIFF_GENERATION>
min_number_of_cliffs 5
max_number_of_cliffs 20  /* map can have 5 to 20 cliffs */
/* other cliff statistics are left to default */

<TERRAIN_GENERATION>
create_terrain WOODS
{
    base_terrain GROUND
    land_percent 5
    number_of_clumps 10
    set_scale_by_groups  /* number of clumps scales: bigger maps have more clumps, of same size */
    set_avoid_player_start_areas  /* we don't like forests around town centers... */
    clumping_factor 1  /* most irregular shapes */
}

create_terrain MED_WATER
{
    base_terrain WATER
    land_percent 10
    number_of_clumps 10  /* number of clumps does not scale: bigger maps have bigger clumps */
    spacing_to_other_terrain_types 3  /* keep away from shores */
}

<CONNECTION_GENERATION>
create_connect_teams_lands  /* connects allies with shallows */
{
    replace_terrain WATER SHALLOW
    terrain_cost WATER 7
    terrain_size WATER 4 2  /* each path on water is 2 to 6 tiles wide */
    replace_terrain MED_WATER SHALLOW
    terrain_cost MED_WATER 15  /* medium water is preferably avoided */
    terrain_size MED_WATER 2 1
}

<OBJECTS_GENERATION>
/* players' personal objects (placed with set_place_for_every_player) */
create_object TOWN_CENTER
{
    set_place_for_every_player
    max_distance_to_players 0  /* in the center of player lands (far from water) */
}

create_object VILLAGER  /* automatically places 3, or 6 for Chinese, etc. */
{
    set_place_for_every_player
    max_distance_to_players 6  /* near town center */
}

create_object VILLAGER  /* this places 2 extra villagers, regardless of race */
{
    number_of_objects 2
    set_place_for_every_player
    max_distance_to_players 8
}

if REGICIDE  /* always place at least a king for regicide! */
    create_object KING
    {
        set_place_for_every_player
        max_distance_to_players 4
    }
endif

create_object GOLD  /* a group of 6 gold mines for everyone */
{
    set_place_for_every_player
    number_of_groups 1
    number_of_objects 6
    set_gaia_object_only  /* NEEDED when you place non-player objects for players */
    min_distance_to_players 10
    max_distance_to_players 12  /* 10 to 12 tiles away from respective player */
    set_tight_grouping  /* mine pieces are close to each other */
}

/* general map objects, not linked to a specific player */
create_object TREE
{
    number_of_objects 20
    set_scaling_to_map_size  /* a large map has 20 trees; other sizes scale */
    temp_min_distance_group_placement 10 /* keeps trees 10 tiles way from the next tree */
    min_distance_group_placement 2 /* keeps all future objects 2 tiles away from these trees */
}

create_object DEER
{
number_of_groups 5
number_of_objects 3
group_variance 1  /* each group can have 2 to 4 deers */
set_scaling_to_map_size  /* scales only number of groups */
min_distance_to_players 20  /* at least 20 tiles from the center of every land */
}

create_object RELIC
{
number_of_objects 2
set_scaling_to_player_number  /* total relics = 2 x player number */
max_distance_to_other_zones 5  /* keep away from shores */
temp_min_distance_group_placement 5  /* keep away from each other, */
place_on_specific_land_id 111  /* only on the "relic isle"! */
}

/* there's no predefined name for perch fish */
/* actually, there is! It’s FISH */
/* lol */
#const Perch[Fish] 53

create_object Perch[Fish]
{
    number_of_objects 20
    set_scaling_to_map_size
    terrain_to_place_on MED_WATER  /* only on medium water */
}

create_object ARCHER
{
    start_random
    percent_chance 70  /* 2 archers 70% of the times */
    number_of_objects 2
    percent_chance 30  /* one group of 5 archers 30% of the times */
    number_of_groups 1
    number_of_objects 5
    end_random
    set_gaia_object_only  /* rescuable units */
    min_distance_to_players 20
}

if SUMMER
    create_object FLOWER_BED  /* create 1 flower bush, only if it's summer */
    {
         /* no attributes! but the brackets are needed anyway */
    }
endif
```
