本篇主要是針對發表系列文的構成做說明，也會把各篇比較重要的譯注/註再複製一份過來集中作為方便參考之用，以及在最後附上翻譯術語對照表。

另外，在系列文全部發表完之前，有時候在翻譯上尚未能融會貫通，無法保證各篇文章在發表後就是終稿。敝人預計整系列翻譯完全，要製作 PDF 檔案前，會再將整份指南修正、潤稿過一次。若是在這之前有什麼翻譯的不妥之處，還請留言或來信告知、討論，感激不盡。

## 發表順序

因為《隨機地圖腳本指南》各章節的內容多寡不一，為了能穩定產出翻譯，本系列翻譯文在發表時不會以「章」為單位，而是根據內文長度決定是以章、或是節為一篇文章去發表。系列構成大概會是這樣：

1. 《隨機地圖腳本指南》[在翻譯之前]
1. 《隨機地圖腳本指南》翻譯說明 (本篇)
1. 《隨機地圖腳本指南》[緒論]
1. 《隨機地圖腳本指南》[Ch1: 語言]
1. 《隨機地圖腳本指南》Ch1.1: Scheme of a RMS
1. 《隨機地圖腳本指南》Ch1.2.1: `<PLAYER_SETUP>`
1. 《隨機地圖腳本指南》Ch1.2.2: `<LAND_GENERATION>`
1. 《隨機地圖腳本指南》Ch1.2.3: `<ELEVATION_GENERATION>`
1. 《隨機地圖腳本指南》Ch1.2.4: `<CLIFF_GENERATION>`
1. 《隨機地圖腳本指南》Ch1.2.5: `<TERRAIN_GENERATION>`
1. 《隨機地圖腳本指南》Ch1.2.6: `<CONNECTION_GENERATION>`
1. 《隨機地圖腳本指南》Ch1.2.7: `<OBJECTS_GENERATION>`
1. 《隨機地圖腳本指南》Ch1.2.8: Map Sizes
1. 《隨機地圖腳本指南》Ch1.2.9: AI Info
1. 《隨機地圖腳本指南》Ch1.3: General Syntax
1. 《隨機地圖腳本指南》Ch2: TERRAINS & OBJECTS
1. 《隨機地圖腳本指南》Ch3: TESTING
1. 《隨機地圖腳本指南》Ch4: EXAMPLE SCRIPT
1. 《隨機地圖腳本指南》Ch5: LINKS AND RESOURCES

<!--more-->


## 翻譯術語對照表
### 一般術語
- attributes（屬性）
- cliffs（峭壁）
- command（命令）
- elevation（海拔）
- feature（特徵）
- hills（山丘）
- instructions（指令）
- land（土地）
- random map（隨機地圖）
- scenario（劇情）
- script（腳本）
- sea（海洋）
- section（章節）
- terrain（地形）

### 特殊名詞
- Random Map Scripts（隨機地圖腳本）
- Random Map Scripting Guide（隨機地圖腳本編寫指南）
- standard RMS guide（標準隨機地圖腳本）

## 譯注/註一覧

### instructions & command
本系列文把 instructions 翻譯為指令，command 翻譯為命令。兩者不同之處為指令是有附帶資訊、敘述的，針對一個命令再加以說明，也就是大括號裡的屬性（attributes）；而命令則只是單純透過腳本要求地圖產生程序去做什麼事，除了基本參數外，沒有再附加屬性。簡而言之，在本文中，指令可視為一個命令再附加屬性，指令算是命令的一種。另外，關於英文中 instructions 與 command 的差異，有興趣的可以參見這篇簡短說明：[〈Command vs Instruction - What's the difference?〉](http://wikidiff.com/command/instruction)。

### eye-candy
eye candy 在 Google 翻譯裡被翻譯成「秀色可餐」，但是 Oxford 給出的解釋是「a person or thing that is attractive but not intelligent or useful」，也就是「指雖有吸引力，但沒什麼能力或用處的人或事物」，顯然前者的解釋並沒有很完整的把意思表達出來，漏掉了略帶貶義的意思（所以別拿這詞去稱讚別人，小心得罪人 XD）。在看了 Oxford 給出的解釋，我下意識想到的詞就「花瓶」，也就是指人外表看起來很漂亮，但實際上就像花瓶一樣，雖然中看，但裡頭卻是中空的，沒什麼內涵。

雖然理解了這個詞的意思，但在指南的翻譯作業裡，該怎麼翻成符合使用情境的詞，就是另一個需要克服的難題了。有想到幾個詞，有類似的意思但實際上卻不適合用在這裡，像是「紙老虎」、「海市蜃樓」、「虛有其表」、「金玉其外，敗絮其中」，雖然這些詞有類似的意思，但在細節上卻相差甚遠，另一方面是這些詞貶意都太重了，eye candy 感覺並沒那麼強調其不好的部分，反而是下意識想到的「花瓶」還比較對味，但直接寫翻成這詞，又跟指南的風格有所差異。

困擾之時，在噗浪上[發了個噗（好友限定）](https://www.plurk.com/p/mfkuv5)詢問好友們的意見，根據這個單字在我提供的前後文的情境，給了些建議，像是「然並卵（？）」、「只是好看但是並沒有什麼效果」、「只是中看不中用」、「放好看的」、「花瓶」、「視覺效果」或是「裝飾用途」。也建議說「不過也未必一定要翻譯名詞對名詞」，不用太執著於同個單字在一篇指南裡都使用同個翻譯，如果不是專有名詞，可以依照前後文情境在翻譯上做變化，這個想法倒也讓我離開了鬼打牆。

所以關於這個單字我不會都使用同個翻譯詞，而會依照情境做變化去翻成：「純裝飾無實用的物件」、「放好看的」等詞，並不再翻譯後附上括號附註原文。

[在翻譯之前]: https://blog.fntsr.tw/articles/2017/01/24/aoe2-before-translate-rmsg/
[緒論]: https://blog.fntsr.tw/articles/2017/01/28/aoe2-rmsg-introduction/
[Ch1: 語言]: https://blog.fntsr.tw/articles/2017/09/25/aoe-ii-rmsg-ch1-language-reference/
