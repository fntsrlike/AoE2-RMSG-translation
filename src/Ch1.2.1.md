<!--
世紀帝國 II 系列：《隨機地圖腳本指南》CH1.2.1: `<PLAYER_SETUP>` 章節
AOE II: RMSG CH1.2.1 - <PLAYER_SETUP> Section
-->

本文件譯自 [Bultro] 和 [Zetnus] 所編寫的[《Updated New RMS Guide (v2.0.0)》][Guide]，並取得作者同意以標示名稱為翻譯授權。

[Guide]: http://aok.heavengames.com/cgi-bin/forums/display.cgi?action=ct&f=28,42485,0,365
[Bultro]: http://aok.heavengames.com/blacksmith/showprofile.php?author=Bultro
[Zetnus]: http://steamcommunity.com/id/zetnus

本文講述 `<PLAYER_SETUP>` 章節可使用的命令。因為本文內容較少，且 1.2.9 節講述的也是 `<PLAYER_SETUP>` 的命令，遂將兩節合併為一篇文章。

## 正文

### 玩家放置方式
`<PLAYER_SETUP>` 預設都是隨機放置（`random_placement`）的。

#### 隨機放置
```text
random_placement
```
就算你沒有輸入這個指令，作為預設值，它還是會被套用。

#### 同隊相鄰放置
```text
grouped_by_team
```
隊伍成員在地圖上的位置是會比較靠近。這個指令和 `random_placement` 是互斥的。在`create_player_lands` 敘述中的 `base_size` 屬性決定同隊玩家之間的距離。本指令只適用於 UP/HD。

### 游牧型地圖資源修正
```text
nomad_resources
```
修改起始資源以和內建的游牧地圖相符。這代表著城鎮中心的建造成本(275木，100石)會回歸到玩家的資源庫存中。在非游牧類型的地圖也可以使用本指令。本指令只適用於 UP/HD。

<!--more-->

### AI

```text
/* ai_info_map_type <地圖類型> */
ai_info_map_type TYPE
```
本命令屬於選填命令，用來協助 AI（電腦）偵測地圖類型，例如：

```text
/* 本命令告訴 AI 本腳本會產生類似阿拉伯的地圖。 */
ai_info_map_type ARABIA
```

目前有以下選項可以使用：

- ARABIA
- ARCHIPELIGO
- ARENA
- BALTIC
- BLACK_FOREST
- COASTAL
- CONTINENTAL
- CRATER_LAKE
- FORTRESS
- GHOST_LAKE
- GOLD_RUSH
- HIGHLAND
- ISLANDS
- MEDITERRANEAN
- MIGRATION
- MONGOLIA
- NOMAD
- OASIS
- REAL_WORLD_[NAME]
- RIVERS
- SALT_MARSH
- SCANDINAVIA
- SCENARIO
- YUCATAN

#### HD/UP 版本新增的功能與內容
```text
/* ai_info_map_type <地圖類型> <游牧與否> <密林與否> <特殊與否> */
ai_info_map_type TYPE N N N
```
N 代表地圖的風格。1 用來套用風格，0 則是不使用該風格。

1. 第一個數字參數為 1 時，代表此地圖為游牧風格，反之則為 0。
2. 第二個數字參數為 1 時，代表此地圖為密林風格，反之則為 0。
3. 第三個數字參數為 1 時，代表此地圖為特殊風格，反之則為 0。

- 游牧風格是指以沒有城鎮中心為開局的的任何地圖。
- 密林風格是指同隊玩家完全被森林隔絕，必須砍伐穿越才能相遇。
- 特殊風格用來創造會特別偵測此地圖的特殊 AI

舉例來說，一個黑森林游牧地圖應該會這樣設定：
```text
ai_info_map_type BLACK_FOREST 1 0 0
```

在《失落的帝國》以及其之後的資料片（目前統計到《非洲王國》），新增了數種地圖類型：

- STEPPE
- BUDAPEST
- VALLEY
- ATLANTIC
- LAND_OF_LAKES
- LAND_NOMAD
- CENOTES
- GOLDEN_HILL
- MEGARANDOM
- MICHI
- AMBUSH
- CUSTOM
- NILE_DELTA
- MOUNTAIN_PASS
- SERENGETI
- SOCOTRA
- KILIMANJARO

記住，此命令只會幫助已經針對給予地圖類型設計腳本的 AI 做反應，如果你設計的地圖與上述的地圖類型完全不相像，建議是不要使用此命令。

另外，大多數的 AI 還未針對《失落的帝國》以及其之後資料片的地圖去設計如何反應，如果遇到這種情況，你可能要改使用原版中比較適合的 AI 地圖類型。

## 隊伍群落與同隊相鄰之差異

注意，同隊相鄰（`grouped_by_team`）命令和「隊伍群落（Team Together）」的效果是不一樣的。「隊伍群落」是在隨機決定玩家土地（位置）後，再將同一隊伍的玩家分配在同一區的隨機位置上。本命令是**基於隊伍群落的設定上**，再讓同隊玩家的位置更加緊密，幾乎沒有緩衝地帶而直接相鄰，詳細可參見下圖：

[![][阿拉伯]][阿拉伯]
**圖 2-1**：阿拉伯

[![][阿拉伯_隊伍群落]][阿拉伯_隊伍群落]
**圖 2-2**：阿拉伯，隊伍群落

[![][阿拉伯_隊伍群落_同隊相鄰]][阿拉伯_隊伍群落_同隊相鄰]
**圖 2-3**：阿拉伯，隊伍群落，同隊相鄰

[![][阿拉伯_同隊相鄰]][阿拉伯_同隊相鄰]
**圖 2-4**：阿拉伯，同隊相鄰


## 示例
本結摘錄遊戲內建的標準隨機地圖腳本的內容作為示例：

### 阿拉伯
網路對戰常見隨機地圖，標準的設定。

```text
<PLAYER_SETUP>
  random_placement
  ai_info_map_type ARABIA 0 0 0
```

[![][阿拉伯_隊伍群落]][阿拉伯_隊伍群落]
**圖 3-1**：阿拉伯，隊伍群落

### 要塞（Fortress）
就算是要塞，感覺同盟會在隔壁，彈者只是隊伍群落的效果，不算 `grouped_by_team`。

```text
<PLAYER_SETUP>
  random_placement
  ai_info_map_type FORTRESS 0 0 0
```

[![][要塞_隊伍群落]][要塞_隊伍群落]
**圖 3-1**：要塞，隊伍群落

### 黑森林（Black Forest）
儘管森林很多，但是因為道路沒阻絕，所以不算密林風格。

```text
<PLAYER_SETUP>
  random_placement
  ai_info_map_type FORTRESS 0 0 0
```

[![][黑森林_隊伍群落]][黑森林_隊伍群落]
**圖 3-1**：黑森林，隊伍群落

### 游牧（Nomad）
標準游牧地圖，有使用到 `nomad_resources` 命令，以及 AI 的游牧參數為 `1`。

```text
<PLAYER_SETUP>
  random_placement
  nomad_resources
  ai_info_map_type NOMAD 1 0 0
```

[![][游牧_隊伍群落]][游牧_隊伍群落]
**圖 3-1**：游牧，隊伍群落

### 鹽沼地（Salt Marsh）
其實是有提供 SALT_MARSH 的 AI，但腳本裡沒特別設定。

```text
<PLAYER_SETUP>
  random_placement
```

[![][鹽沼地_隊伍群落]][鹽沼地_隊伍群落]
**圖 3-1**：鹽沼地，隊伍群落

### 團隊群島（Team Islands）
同要塞，儘管同盟都在同一座島上，但是仍沒使用到 `grouped_by_team` 命令。
```text
<PLAYER_SETUP>
  random_placement
  ai_info_map_type TEAM_ISLANDS 0 0 0
```

[![][團隊群島_隊伍群落]][團隊群島_隊伍群落]
**圖 3-1**：團隊群島，隊伍群落

## 結論
`<PLAYER_SETUP>` 主要是設定遊戲者（玩家、電腦 AI）的位置，以及初始的相關設定，像是游牧資源特殊設定、電腦 AI 的設定等。除了翻譯外，本文也針對「隊伍群落」和「同隊相鄰」有可能混淆的部分做了補充，更附上內建標準隨機地圖腳本的此章節的程式碼與實際產生後地圖的迷你地圖截圖作比較，希望能讓大家更近一步的了解。然而此章節只是訂定大方向的位置放置策略，事實上在後面的章節仍有許多因素會影響遊戲者的位置，這是另外要注意的事，詳細的部分就等之後翻譯到相關篇章時再做說明了。


[阿拉伯]: https://blog.fntsr.tw/wp-content/uploads/2017/09/阿拉伯.png
[阿拉伯_隊伍群落]: https://blog.fntsr.tw/wp-content/uploads/2017/09/阿拉伯_隊伍群落.png
[阿拉伯_隊伍群落_同隊相鄰]: https://blog.fntsr.tw/wp-content/uploads/2017/09/阿拉伯_隊伍群落_同隊相鄰.png
[阿拉伯_同隊相鄰]: https://blog.fntsr.tw/wp-content/uploads/2017/09/阿拉伯_同隊相鄰.png
[要塞_隊伍群落]: https://blog.fntsr.tw/wp-content/uploads/2017/09/要塞_隊伍群落.png
[黑森林_隊伍群落]: https://blog.fntsr.tw/wp-content/uploads/2017/09/黑森林_隊伍群落.png
[游牧_隊伍群落]: https://blog.fntsr.tw/wp-content/uploads/2017/09/游牧_隊伍群落.png
[團隊群島_隊伍群落]: https://blog.fntsr.tw/wp-content/uploads/2017/09/團隊群島_隊伍群落.png
[競技場_隊伍群落]: https://blog.fntsr.tw/wp-content/uploads/2017/09/競技場_隊伍群落.png
[鹽沼地_隊伍群落]: https://blog.fntsr.tw/wp-content/uploads/2017/09/鹽沼地_隊伍群落.png
