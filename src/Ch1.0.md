<!--
世紀帝國 II 系列：《隨機地圖腳本指南》CH1: 語言
AOE II: RMSG CH1 - Language Reference
-->

本文件譯自 [Bultro] 和 [Zetnus] 所編寫的[《Updated New RMS Guide (v2.0.0)》][Guide]，並取得作者同意以標示名稱為翻譯授權。

[Guide]: http://aok.heavengames.com/cgi-bin/forums/display.cgi?action=ct&f=28,42485,0,365
[Bultro]: http://aok.heavengames.com/blacksmith/showprofile.php?author=Bultro
[Zetnus]: http://steamcommunity.com/id/zetnus

本文章主要在講述腳本基礎架構，以及在編寫時應注意的細節。

## 正文

腳本 (scripts) 共分為七個章節（section），各章節專職一種地圖特徵（feature）。章節透過下列標籤 (tags) 的宣告作為起始：

<div class="table"></div>

**表 1：**章節起始宣告關鍵字一覧

| 章節名稱                   | 用途 |
| ---                       | --- |
| `<PLAYER_SETUP>`          | 基本設定 |
| `<LAND_GENERATION>`       | 土地設定，主要土地 (lands) 或海洋 (sea) |
| `<ELEVATION_GENERATION>`  | 山丘 (Hills) |
| `<CLIFF_GENERATION>`      | 峭壁 (Rocky cliffs) |
| `<TERRAIN_GENERATION>`    | 地形 (Terrain) |
| `<CONNECTION_GENERATION>` | 連接地形，像是道路、橋 |
| `<OBJECTS_GENERATION>`    | 單位、建築、資源、無用途的裝飾物件（放好看的） |

<!--more-->

- 你不需要按照上面的順序去編寫腳本的章節，但是遊戲程式會按照上面的順序去讀取章節以建立地圖。
- 你可能會注意到遊戲內建的標準地圖在峭壁和連接地形的章節有不同的順序（有時包括海拔的章節）。然而，依照上面的順序去編寫，會讓你對地圖產生程序的想像以及了解發生了什麼事有所幫助。像是水可能會生成在山丘上、物件會被放置在連接地形上、或是為什麼地形可以避開峭壁等細節，這些都跟地圖在各特徵產生的順序有所關係。但無論如何，你編寫章節的順序都不會讓對地圖的產生造成差異。
- 不是所有章節都是需要的（像是你可以建立一個沒有峭壁的地形）。
- 每個章節都會有不同種類的指令 (instructions)[^instructions and command]，多數的指令大概像是這樣：

```text
create_something WHAT
{
    attribute TYPE
    attribute N
    set_attribute
    ...
}
```

- 在編寫腳本時，你可以隨你所欲的對指令內容進行縮排。只要將關鍵字透過換行（new line）或空白 (space) 進行分隔即可。
- 腳本的關鍵字與常數名稱對大小寫敏感，請注意字母的大小寫。
- 所有 `create` 命令都是可以使用多次的，其他命令則只能使用一次。
- 多數屬性 (attributes)（也就是在大括號裡的次要命令(subcommands)）都會有預設值，不用特地寫出來。所以在有些時候，大括號 `{ }` 中是可以留白的！
- 大括號裡屬性的順序也是不重要的，其排序對地圖的產生沒有影響。
- 如果有項目因為某些原因無法被建立，那遊戲程式會直接忽略它並繼續往下讀取。如果你發現有東西不見了，請嘗試稍微放寬其放置的限制 (constraints)。


## 筆記、摘要
- 七個章節：玩家、土地、海拔、峭壁、地形、連接、物件。
- 程式會照順序讀取章節並逐一生成地圖特徵。
- 腳本章節編寫順序不影響地圖生成；指令內屬性順序不影響生成效果。
- 關鍵字和常數大小寫敏感。

[^instructions and command]: 本系列文把 instructions 翻譯為指令，command 翻譯為命令。兩者不同之處為指令是有附帶資訊、敘述的，針對一個命令再加以說明，也就是大括號裡的屬性（attributes）；而命令則只是單純透過腳本要求地圖產生程序去做什麼事，除了基本參數外，沒有再附加屬性。簡而言之，在本文中，指令可視為一個命令再附加屬性，指令算是命令的一種。另外，關於英文中 instructions 與 command 的差異，有興趣的可以參見這篇簡短說明：[〈Command vs Instruction - What's the difference?〉](http://wikidiff.com/command/instruction)。
