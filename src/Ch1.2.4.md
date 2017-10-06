
#### 1.2.4. <CLIFF_GENERATION>

峭壁是不可行走的岩石峽谷。你不能建立單一個峭壁，但是你可以定義通用峭壁的統計資訊。
所有命令都有合理的預設值。只要單純輸入 `<CLIFF_GENERATION>` 就足以建立一班的峭壁。如果你不希望你的地圖擁有峭壁，那就不要放置 `<CLIFF_GENERATION>` 章節關鍵字。峭壁會自動避開玩家的起始區域，以及非玩家土地的中心地帶。

##### Commands
```
min_number_of_cliffs N
max_number_of_cliffs N
```
峭壁數量的最大值。峭壁沒辦否根據地圖大小去自動調整。（但你可以透過 `if` 手動調整其在指定大小的地圖中擁有的數量）

```
min_length_of_cliff N
max_length_of_cliff N
```
各峭壁長度的最大值和最小值。（每個峭壁會有不同的長度）

```
cliff_curliness %
```
給個峭壁單位可能會轉彎的機率。% 越低，就會生成較直的峭壁，越高就會容易生成迂迴折曲的峭壁。

```
min_distance_cliffs N
```
每個峭壁之間的最小距離，以格數為單位。預設值為 2。
Minimum distance between cliffs, in tiles. Default is 2.

```
min_terrain_distance N
```
距離水或冰地形的最小距離。本屬性並不套用在 `<TERRAIN_GENERATION>` 章節中生成的水。預設值為 2。
