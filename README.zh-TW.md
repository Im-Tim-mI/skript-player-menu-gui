# 玩家選單 GUI

[English](README.md) | **繁體中文**

以 Shift + F（或 `/menu`、`/選單`）開啟的箱子 GUI 快捷選單：傳送主城／回家、瀏覽遊戲世界與玩家世界、用鐵砧輸入框建立世界、世界編輯者專用的 WorldEdit 工具、骰子，以及完整的大富翁操作面板。

> 本儲存庫包含同一個腳本的兩個版本：**繁體中文（zh-TW）** 是作者伺服器實際使用的原始版本；**English** 為完整英文翻譯版（指令、訊息與變數名稱皆為英文），功能相同。

<!-- BEGIN LIVE SCREENSHOTS -->

## 畫面預覽

![主選單箱子介面](docs/images/player-menu-gui.png)

*以一般玩家身分執行 `/menu`：伺服器實際送出的 3 列「主選單」箱子介面（`generic_9x3`，5 個按鈕）。*

![主選單與物品提示框](docs/images/player-menu-gui-tooltip.png)

*同一個選單並停留在第一個按鈕上。物品名稱與說明文字皆為 `window_items` 封包的實際內容。*

> 這些是實機擷取後重繪的畫面，不是原生客戶端截圖。流程為：無頭客戶端登入實機 Paper 26.2 伺服器觸發腳本，再以官方 Minecraft 26.2 客戶端素材忠實重繪伺服器回傳的方塊／介面資料。Mojang/Microsoft 的圖像資產不屬於本專案程式碼授權範圍。

<!-- END LIVE SCREENSHOTS -->

## 功能特色

- Java 版蹲下 + 切換副手（F）、基岩版蹲下 + 表情（需搭配 EmoteOffhand 等把表情轉成切換副手的 Geyser 擴充），或輸入 `/menu`、`/選單` 開啟
- 傳送主城／回家，以及可一鍵傳送的遊戲世界與玩家世界列表
- 情境按鈕：在自己的玩家世界時顯示小木斧、模式切換、WorldEdit 教學書與刪除世界；管理員在遊戲世界時顯示刪除遊戲世界
- 用鐵砧輸入框輸入名稱建立世界（skript-anvil-input-api）
- 內建玩家世界使用手冊與 WorldEdit 教學書
- 在 `game_12` 內提供大富翁面板：擲骰、現金、排行、起點、繳稅、抽卡、付錢給玩家，以及管理員銀行工具

## 需求

- [Paper](https://papermc.io/) 伺服器（開發環境 Paper 26.2 / Minecraft 26.2）
- [Skript](https://github.com/SkriptLang/Skript)（開發環境 2.16.2）
- [skript-reflect](https://github.com/SkriptLang/skript-reflect)（開發環境 2.6.3）
- [skript-player-game-worlds](https://github.com/Im-Tim-mI/skript-player-game-worlds)－**必要**（`pw_base()`、`canEdit()`）
- [skript-anvil-input-api](https://github.com/Im-Tim-mI/skript-anvil-input-api)－**必要**（`openAnvilInput()`、`on anvil input`）
- [skript-game-world-manager](https://github.com/Im-Tim-mI/skript-game-world-manager)、[skript-monopoly-helper](https://github.com/Im-Tim-mI/skript-monopoly-helper)、[skript-dice-roller](https://github.com/Im-Tim-mI/skript-dice-roller)－按鈕會執行它們的指令
- [EssentialsX](https://essentialsx.net/)（`/spawn`、`/home`）
- [WorldEdit](https://enginehub.org/worldedit)

## 安裝

1. 先安裝[需求](#需求)中列出的插件。
2. 下載**其中一個**版本：

   | 版本 | 檔案 |
   |---|---|
   | 繁體中文（原始版本） | [`zh-TW/玩家選單GUI.sk`](zh-TW/%E7%8E%A9%E5%AE%B6%E9%81%B8%E5%96%AEGUI.sk) |
   | English（英文） | [`en/player-menu-gui.sk`](en/player-menu-gui.sk) |

3. 把 `.sk` 檔案放進伺服器的 `plugins/Skript/scripts/`。
4. 執行 `/sk reload 玩家選單GUI`（請換成你放入的檔名），或重新啟動伺服器。

> [!IMPORTANT]
> **只能安裝其中一個版本。** 兩個版本是同一個腳本的不同語言，同時載入會互相衝突或重複執行。

## 指令

| 指令（中文版） | 英文版 | 說明 | 權限 |
|---|---|---|---|
| `/menu`、`/選單` | `/menu` | 開啟主選單 | 所有人 |
| Shift + F（蹲下 + 切換副手） | Shift + F (sneak + swap hands) | 開啟主選單 | 所有人 |

## 設定

- `isAdmin()` 決定誰能看到管理員按鈕：OP 或擁有 `menu.admin` 權限。
- 大富翁按鈕只在 `game_12` 世界出現，若使用其他世界請搜尋並修改。
- 教學書的作者為 `rr901037`，可修改 `set book author` 那幾行。

## 注意事項

- 所有相關腳本請使用同一語言版本：選單會執行它們的指令（`/玩家遊戲世界列表`、`/遊戲世界列表`、`/一顆骰字`、`/roll`……）並讀取它們的變數。
- 選單以視窗標題（例如「主選單」）辨識，請避免其他插件使用相同標題。
- 中文版的大富翁按鈕呼叫英文別名（`/roll`、`/pay`……）；英文版則呼叫完整的 `monopoly_` 指令名稱。

## 相關專案

- [skript-player-game-worlds](https://github.com/Im-Tim-mI/skript-player-game-worlds)－玩家遊戲世界管理系統
- [skript-anvil-input-api](https://github.com/Im-Tim-mI/skript-anvil-input-api)－鐵砧輸入框 API
- [skript-game-world-manager](https://github.com/Im-Tim-mI/skript-game-world-manager)－遊戲世界管理系統
- [skript-monopoly-helper](https://github.com/Im-Tim-mI/skript-monopoly-helper)－大富翁小幫手
- [skript-dice-roller](https://github.com/Im-Tim-mI/skript-dice-roller)－自動化骰子
- [skript-discord-link-reminder](https://github.com/Im-Tim-mI/skript-discord-link-reminder)－Discord 綁定提醒

## 授權

**MIT + Commons Clause**，完整條款請見 [LICENSE](LICENSE)。

- ✅ 可自由使用、複製、修改與分享本腳本。
- ✅ 本授權明確允許在收費或營利的 Minecraft 伺服器上安裝與運行本插件（含修改版）。
- ❌ 禁止的僅限於直接或間接販售本插件本體、修改版本，或以付費方式取得其檔案或原始碼。

Copyright (c) 2026 廷廷小教室、廷廷的家（Tim945）
