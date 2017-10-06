#### 1.2.9. AI Info
```
ai_info_map_type TYPE
```
This is an optional line at the start of a script to help the AI (computer player) detect the type of map. For example:

```
ai_info_map_type ARABIA  /* this tells an AI that your map is like Arabia */
```

The following can be used:
```
ARABIA / ARCHIPELIGO / ARENA / BALTIC / BLACK_FOREST / COASTAL / CONTINENTAL / CRATER_LAKE / FORTRESS / GHOST_LAKE / GOLD_RUSH / HIGHLAND / ISLANDS / MEDITERRANEAN / MIGRATION / MONGOLIA / NOMAD / OASIS / REAL_WORLD_[NAME] / RIVERS / SALT_MARSH / SCANDINAVIA / SCENARIO / YUCATAN
```

##### New with HD/UP:
```
ai_info_map_type  TYPE N N N
```
The N values are for map styles. 1 is used if the style applies, 0 if it does not apply.
The 1st number is 1 if nomad, else 0
The 2nd number is 1 if michi, else 0
The 3rd number is 1 if extra style, else 0
- Nomad is any map where you start without a town center
- Michi is a type of map where teams are completely separated from each other by forest and have to cut through.
- Extra Style can be used to create a special AI which will specifically detect your map.

Example – a black forest nomad map would be:
```
ai_info_map_type BLACK_FOREST 1 0 0
```

There are several new map types defined for The Forgotten and African Kingdoms:
```
STEPPE / BUDAPEST / VALLEY / ATLANTIC / LAND_OF_LAKES / LAND_NOMAD / CENOTES / GOLDEN_HILL / MEGARANDOM / MICHI / AMBUSH / CUSTOM / NILE_DELTA / MOUNTAIN_PASS / SERENGETI / SOCOTRA / KILIMANJARO
```

Remember – these will only help the AI if that AI has actually been scripted to respond to a given map label. If your map is not very similar to any of these maps, it may be best to leave out ai_info_map_type.
Also, most AIs will not be coded to respond to the new AoF/AK map definitions, so you may want to pick a suitable map from the Conquerors list instead.

