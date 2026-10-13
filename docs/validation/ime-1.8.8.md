# 1.8.8 輸入法組字更新修復

Compose 1.10.1 會在 `LegacyPlatformTextInputServiceAdapter.skiko.kt` 中，將一個 `TextEditingScope` 區塊拆成個別的 `onEditCommand` 呼叫。組字更新先執行 `CommitText("")`，再執行 `SetComposingText(remaining)`。第一個回呼會讓應用程式看見已清空的組字文字與空的組字範圍，第二個回呼才恢復內容。

上游實作目前會先收集指令，再一次呼叫 `onEditCommand(commands)`。Hermes 透過公開的 `InterceptPlatformTextInput` API 回補這個批次處理方式，範圍限於三個 macOS 輸入框。沒有替換框架類別或原生函式庫。刪除操作仍由原生輸入法處理；應用程式不重建拼音。

檢查的上游原始碼：

- https://github.com/JetBrains/compose-multiplatform-core/blob/v1.10.1/compose/foundation/foundation/src/skikoMain/kotlin/androidx/compose/foundation/text/input/internal/LegacyPlatformTextInputServiceAdapter.skiko.kt
- https://github.com/JetBrains/compose-multiplatform-core/blob/568b08af72b029e2622dd47c727de50aa547a68b/compose/foundation/foundation/src/skikoMain/kotlin/androidx/compose/foundation/text/input/internal/LegacyPlatformTextInputServiceAdapter.skiko.kt

驗證分成三個部分：

1. 批次語意：每次原生編輯只產生一個可觀察狀態，並涵蓋部分提交、明確取消與中止編輯。
2. AWT 整合：使用真實 Compose 視窗，在每個輸入法事件期間檢查暫態；只停用批次處理，以證明回歸檢查能抓出 1.8.7 的行為。
3. 實際 macOS 輸入：可選擇執行 Robot → 系統拼音 → Cocoa → AWT 測試。WeType 是獨立測試；macOS 無法選用它時會明確跳過。系統拼音測試通過，不代表 WeType 通過。

使用者回報 1.8.6／1.8.7 未修復 WeType 刪除整段組字文字的問題。CI 的 macOS 15.7.9 在確認 WeType 2.2.3 安裝成功後，仍拒絕選用它，回傳 OSStatus -50。批次處理缺陷已獨立確認；在能正常使用 WeType 的環境完成測試前，尚不能確認它與使用者遇到的問題完全相同。

「說明 → 輸入法診斷」視窗需自行開啟。它僅在記憶體中保留自己視窗的最多 500 筆中繼資料事件，記錄長度、範圍、編輯按鍵代碼、執行環境版本及時間，不記錄輸入文字，也不上傳資料。複製需要點選按鈕；關閉視窗會移除監聽器並丟棄緩衝區。
