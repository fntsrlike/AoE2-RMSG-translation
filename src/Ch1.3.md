  ### 1.3. General Syntax
These structures can be used anywhere in an RMS. Most of them allow a RMS to change at every game.

#### 1.3.1. Comments
```
/* This is a comment. It's ignored by the game, but useful to people who read the RMS, especially yourself! */
```
-  Comments can span on multiple lines
-  Comments can be nested. Nested comments can occasionally cause weird behavior when nested after #const
-  There must be space or new line between the asterisks and the words, otherwise the whole rest of your script may be ignored!

#### 1.3.2. Conditionals
```
if LABEL_1
  (...)  /* commands executed only if LABEL_1 is defined */
elseif LABEL_2
  (...)  /* commands executed only if LABEL_2 is defined */
elseif LABEL_3
  (...)  /* commands executed only if LABEL_3 is defined */
else
  (...)  /* commands executed only if none of the previous labels is defined */
endif
```

Commands following an "if" statement (until next elseif/else/endif) are executed ONLY if respective LABEL is true.
E.g. Kings should be created only if game mode is Regicide.

-  "elseif"s and "else" are optional:
  *  elseif checks another condition, if previously checked conditions fail
  *  else executes by default if none of the other conditions apply
-  An if structure can control whole commands, but can also be used inside any { } brackets, to control attributes
-  Whole if structures can be nested
-  A "NOT" can be implemented this way:
```
if LABEL
else
  (...)  /* this code is executed if LABEL is NOT true! */
endif
```

Here are the possible condition labels defined by the game.
- Game type:
  - REGICIDE
  - DEATH_MATCH
- Map dimension:
  - TINY_MAP
  - SMALL_MAP
  - MEDIUM_MAP
  - LARGE_MAP
  - HUGE_MAP
  - GIGANTIC_MAP
  - LUDIKRIS_MAP
- Starting resources:
  - HIGH_RESOURCES
  - MEDIUM_RESOURCES
  - LOW_RESOURCES
  - DEFAULT_RESOURCES
- Player positioning:
  - FIXED_POSITIONS: defined if the "Team Together" box is checked
- UserPatch-only Definitions:
  - RANDOM_MAP: defined for Random Map games
  - TURBO_RANDOM_MAP defined for Turbo Random Map games
  - KING_OT_HILL: defined for King of the Hill games
  - WONDER_RACE: defined for Wonder Race games
  - DEFEND_WONDER: defined for Defend the Wonder games
  - CAPTURE_RELICS: defined for the Relics victory condition
  - [1-8]_PLAYER_GAME: defined as the total number of players (2_PLAYER_GAME, etc.)
  - UP_AVAILABLE: defined for v1.4 and later; used to detect the patch
- AoF/AK-only Definitions:
  CAPTURE_THE_RELIC: Defined for the new "capture the relic" mode

In addition, it is possible to use any of the Item Constants (1.3.4.) in conditionals.  They will always be true if that constant is available in the game.  This can be used to implement conditional checks for mods or DLC.  For example:

```
if BEGUINE /* this is a pre-defined constant in Age of Chivalry */
create_object JAGUAR /* creates a Jaguar if you are using Age of Chivalry */
else
create_object WOLF /* otherwise creates a wolf */
endif
{
}
```

Currently (patch 5.1), this technique cannot be used to distinguish between the basegame in the HD Edition and AoF/AK in the HD Edition because both of them have access to the same full list of constants in the game.

```
#define LABEL
```
Defines whatever label you want, to be used as an if condition. It will evaluate as true.
-  Condition names can contain ANY character (`"$%&òà"` is a valid condition!!)
-  Be careful when choosing a name that is already defined as a constant.  For example #define DESERT caused me problems; probably because DESERT is a preexisting terrain name.


#### 1.3.3. Random Code
```
start_random
percent_chance %
(...)
percent_chance %
(...)
end_random
```
Blocks of code following each percent_chance instruction have that percent probability at each game to be executed.
If percents don't add up to 100, the remaining percent is the chance that nothing happens.
-  Random structures can control whole commands, but can also be used inside { } brackets, to control attributes
-  Whole random structures can be nested
-  You cannot use decimals (percent_chance 12.5 is NOT valid)
Example:
```
start_random
  percent_chance 30
    #define ARABIAN_MAP    /* map will be Arabian in 30% of games */
  percent_chance 20
    #define NORTHERN_MAP  /* map will be northern in 20% of games */
end_random      /* map will be default (e.g. temperate) in remaining 50% of games */
```

#### 1.3.4. Item Constants
```
#const   NAME   N
```
Creates a constant name for a terrain or object type, suitable for commands such as create_terrain.
Items are identified by a number inside the game, but by a name (such as GRASS) in a RMS; this command ties a practical name to an item number. Numbers are reported in "Terrains & Objects" chapter.
-  Constant names can contain ANY character ("$%&kòà" is a valid name!!)
-  Every item can have many names; original names remain valid
-  You can't redefine an existing name to a different number
Most items already have a predefined name, anyway #const can be very useful because:
-  Some items, e.g. snowy road, don't have a predefined name
-  You may want an alias for your convenience, e.g. in your language
-  You can define variable items with a single if structure, instead of checking every time an item is used.
In this example you would use only GROUND and TREE from now on:
```
If ARABIAN_MAP
  #const GROUND 14  /* desert */
  #const TREE 351  /* palm */
elseif NORTHERN_MAP
  #const GROUND 32  /* snow */
  #const TREE 413  /* snowy pine */
else
  #const GROUND 0  /* grass */
  #const TREE 411  /* oak */
endif
```

`#const` works only for terrain and object identifiers, not generic numbers. You CAN'T do this:

```
#const NUM 10
(...)
number_of_objects NUM
```
