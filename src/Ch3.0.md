Chapter 3. TESTING
---

You'll have to do lots of tries before your RMS works fine... Sadly, the "Generate Map" button in the Scenario Editor doesn't work for custom maps, so you have to set up test games in "All Visible" mode to see your map.
Note that if you click "Restart Game", the random seed won't be changed, that is: it will generate exactly the same map! If you minimize the game (alt + tab), modify the RMS, then click Restart Game, only the things you modified will actually change. If you want to see a completely different output of your RMS, you need to click "End Game" and then set up a new game again (yeah, very boring...).

##### Update:
The UP and HD both give you the capability of generating custom RMS in the Scenario Editor, using the "Generate Map" button! So there is no need to start a new game for each test anymore. You can also select a specific seed if you want to test with the same seed. The only reason to test an actual game is if you need to see what team lands look like, because the scenario editor treats all players as being on separate teams.

##### Warning:
Occasionally things will generate slightly differently in the Scenario Editor than they will in-game. For example: resource_delta doesn’t work, player objects on water behave differently and a few AoF units are invisible. Most importantly, every player is always on their own team for the purposes of map generation in the Scenario Editor.  Thus you need to test team lands and team connections in-game instead of in the Scenario Editor.

## 3.1. Editing gamedata_x1.drs (unnecessary since the release of the UP or HD Edition)
This allows custom RMS to be generated with the "Generate Map" button in the Scenario Editor!
However, it's a tricky method and normally I don't recommend it to RMS designers.
gamedata_x1.drs is a file in "Data" subdirectory of the game; it contains the RMS code of standard maps (Arabia, Baltic, etc.). If you open this file with any text editor, you can modify or replace any standard map with your code.
Choose e.g. Arabia, replace it, then restart the game: now when you generate an Arabia map (in a game or in the scenario editor), actually your RMS will be generated.
RMSs in gamedata_x1.drs can have a line that looks like: `#include_drs land_resources.inc 54102`
It creates standard resources, so remove it if you coded your resources. Don't touch other lines you don't know!
-	I think this method is most useful to Scenario designers (but I'm not a Scenario designer :P )
-	It can easily crash the game, so ALWAYS make a backup copy of the original gamedata_x1.drs!
-	You CAN'T play on multiplayer with modified maps
-	It allows to play custom maps even if you don't have The Conquerors expansion! Of course without expansion stuff such as snow... You have to edit gamedata.drs the same way
-	A program called Setup Map (see section 5.3.) can automatically edit and swap gamedata_x1.drs files for you
-	It’s useful to know that you can find a copy of the standard maps simply by opening gamedata_x1.drs with a text editor!

