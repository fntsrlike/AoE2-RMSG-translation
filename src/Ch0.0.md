<!--
世紀帝國 II 系列：《隨機地圖腳本指南》緒論
AOE II: Random Map Scripting Guide - Introduction
-->

本文件譯自 [Bultro] 和 [Zetnus] 所編寫的[《Updated New RMS Guide (v2.0.0)》][Guide]，並取得作者同意以標示名稱為翻譯授權。

[Guide]: http://aok.heavengames.com/cgi-bin/forums/display.cgi?action=ct&f=28,42485,0,365
[Bultro]: http://aok.heavengames.com/blacksmith/showprofile.php?author=Bultro
[Zetnus]: http://steamcommunity.com/id/zetnus

## 正文

隨機地圖腳本（Random Map Scripts）可以定義一般類型的地圖，像是阿拉伯（Arabia）、波羅的海（Baltic）。**千萬不要**把隨機地圖（random map）和劇情（scenario）搞混：隨機地圖在每一場遊戲看起來都不同，而且**不能**使用劇情編輯器去設計。

「標準隨機地圖腳本」位在遊戲的 `DOCS` 子資料夾[^標準隨機地圖腳本]，雖然它有講述細節，但裡面卻有非常多的缺失和錯誤。隨機地圖必須以純文字格式檔案作儲存，並且以 `.RMS` 為副檔名[^副檔名]、名稱全長不得超過 20 字元。雖然超過長度的名字在 HD 版中不會造成遊戲崩潰，但會造成在遊戲中只看得到前面部分的名稱[^中文檔名]。你可以透過任何文字編輯器編寫腳本，像是 Notepad / Notepad++ 或是 Word，只要記得透過「另存新檔」去設置檔案類型為「所有檔案 (*.*)」或是純文字格式。你也可以透過本文件 5.2 節（5.2. Editors and Generators）所提到的任一隨機地圖腳本編輯器或產生器進行編寫。透過這些編輯器程式碼高亮的功能可以幫助你減少錯字！

在原版裡，腳本必須放在 `Random` 的子資料夾。在 HD 版，資料夾則改到 `resources\_common\random-map-scripts`。腳本會在多人連線時，傳送給其他玩家。但如果你有一個使用相同名稱的新版腳本，其他玩家必須手動刪除舊版的檔案。

你必須讓大家知道你的地圖是否適用於單人遊戲，因為遊戲通常不會去區別。只要地圖不要太奇特，電腦 AI 通常可以在自製地圖中玩得很好。請記得電腦 AI 需要以下元素：

- 需要廣闊的建築空間
- 可以簡單地取得所有類型的資源
- 他們不會透過運輸船去運送村民
- 他們不會援助中立單位 [^中立單位]

[^標準隨機地圖腳本]: 這邊指的是官方原版文件。
[^副檔名]: 大小寫不分，但通常還是以小寫 `*.rms` 為主。
[^中文檔名]: 在 HD 版中若以中文命名，會完全看不到名稱。
[^中立單位]: 只有玩家接觸到中立單位，中立單位才會轉換陣營，若是電腦 AI 接觸則會保持中立。
