#### 1.2.6. <CONNECTION_GENERATION>
連結（Connection）是一條連接屬地的線狀地形。通常用來確保單位可以在各土地互通有無。
你無法建立單一連結，只能建立通用系統的連結。如果可能，連結會將串聯個土地的中心點（例如透過 `max_distance_to_players 0` 被放置在土地中心的城鎮中心。

##### Commands
```
create_connect_all_lands  { ... }
```
連結所有土地。一般來說，此指令不包括透過 `<TERRAIN_GENERATION>` 所建立的小島。

```
create_connect_all_players_land { ... }
```
連結所有玩家的土地。如果沒有人的土地處在成本最低的路徑上，那連結也會通過。


```
create_connect_teams_lands { ... }
```
連結同盟內各玩家的土地。如果沒有人的土地處在成本最低的路徑上，那連結也會通過。

```
create_connect_same_land_zones { ... }
```
看起來行為和 `create_connect_all_lands` 是相同的，但因為此指令之前都沒有文件，所以通常不會使用。

##### Attributes

```
default_terrain_replacement TYPE
```


通過用指定的地形替換所有中間地形來創建連接。 以前沒有文件，因此通常不會使用。 如果使用，請確保在任何 `replace_terrain` 屬性之前使用。 那些 `replace_terrain` 屬性可以用於為連接的部分指定不同的地形。 例如，用道路替換所有地形，但是用淺灘替換水。 當在 `replace_terrain` 屬性之後使用它時，它會覆蓋它並重新替換連接上的地形。

```
replace_terrain       TYPE       TYPE
```
定義什麼基礎地形應該被什麼連接地形替換。
通常用淺灘取代水，通過 `replace_terrain WATER SHALLOW`。
預設情況下，連接可以通過未指定的地形，但是如果給定地形沒有 `replace_terrain`，則它們不可見。
如果要確保連接不通過地形，請將該地形賦予相對較高的 `terrain_cost`。
您可以自行替換地形。

```
terrain_cost       TYPE       N(1-15)
```
通過指定地形的成本（就算沒有在 `replace_terrain` 提到，你也可以設置該地形的成本）。連結將會傾向通過較低成本的地形，必且盡量避開成本較高的地形（或是取最短路徑）。預設值是 1。

```
terrain_size          TYPE      N   N
```
連結通過指定地形的寬度（需要搭配 `replace_terrain` 使用）
- 第一個參數代表幾格寬。
- 第二個參數代表連結寬度在每一點上的隨機誤差值。例如 `terrain_size WATER 5 2` 會建立一條 3 ~ 7 寬的道路。此屬性的預設值是 `1 0`。
若將隨機誤差值設置大於連結基礎寬度，可能會產生寬度為 0 的情況（連結中斷）。
如果連結看起來比他應該有的寬度還寬，那有可能是兩條以上的平行連結重疊的端係。要改善此種狀況，可以透過地形成本。
