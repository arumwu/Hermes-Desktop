# Hermes Windows 1.2.0 驗證記錄

構建環境：Linux x64，Temurin JDK 21.0.8+9，Gradle 8.13。應用版本 1.2.0。

## 自動化迴歸

`gradle test --offline`：129 項，127 項通過，0 項失敗，2 項按平臺條件跳過。

逐套件記錄見 `validation/windows-1.2.0-tests.json`。新增覆蓋會話上限、無總數分頁、短頁、重疊頁、重複頁、歸檔分頁、錯誤響應、首頁草稿與附件轉移、模板保留原文及快速查詢上下文。

## 實際元件渲染與互動

`gradle renderPreviews` 使用真實 Compose 元件、演示會話和檔案生成預覽。覆蓋工作臺三套主題、窄視窗、150% / 200% DPI、錯誤與載入狀態、聊天與文件並排、專注模式、快速查詢、設定、技能、語音、訊息、任務、表格與文件差異。

實際操作檢查包括：工作臺輸入→追加模板→開始任務；檔案欄收放與拖動保留會話/文件；長訊息跳到底部；設定未儲存輸入在導航後保留；高 DPI 下主題選擇和滾動到儲存按鈕；會話時間篩選的滑鼠狀態。快速查詢還驗證了輸入篩選、方向鍵、Enter、Esc 和原會話保留。

截圖位於 `previews/windows-1.2.0/`。它們是元件渲染，不是 Windows 真機截圖。

## Windows 包

Windows x64 依賴通過 `stageWindowsApplication -PdesktopTarget=windows-x64` 準備。組裝指令碼檢查 JavaFX Windows 模組、Skiko DLL 和執行環境的 x64 PE 標識，拒絕其他平臺及測試依賴，並檢查歸檔 CRC。

官方執行環境：Eclipse Temurin JRE 21.0.12.1+1 Windows x64。發行商 ZIP SHA-256：

`d35f31e712f0fcf6ac5a093edc90204fbff22f720ba3950bd09d331d5e621636`

更新包只替換 1.1.0 的 `app/hermes-desktop.jar`；執行依賴版本保持一致。完整包內 `manifest.json` 記錄每個 JAR 的 SHA-256。

## 平臺邊界

沒有在 Windows 真機執行本包；未測試真實閘道器賬號、麥克風、Windows 系統語音、系統通知、DPAPI 或 JavaFX 原生視窗。也沒有新做 macOS 真機驗收。Windows 啟動失敗時請執行 `Diagnose-Hermes.bat` 並檢視日誌。
