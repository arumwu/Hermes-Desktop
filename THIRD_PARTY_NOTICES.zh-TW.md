# 來源與第三方資源

- Hermes 的協定、資料模型、部分解析邏輯、品牌圖示、頭像與人物素材來自使用者提供的 `hermes-assistant-2.zip`，其 README 標記 Android 版本為 3.6.5。此適配不替原專案或品牌資產重新指定授權，也不包含原 Android 簽章私鑰。
- 匯出的原專案圖示包含 Phosphor Icons 資源，保留原專案中的 MIT 授權全文：`licenses/Phosphor-MIT.txt`。
- 隨附字型 `NotoSansCJKsc-Regular.otf` 來自 [notofonts/noto-cjk](https://github.com/notofonts/noto-cjk/tree/main/Sans)，字型授權全文：`licenses/NotoSansCJK-OFL.txt`。未修改字型。
- 應用程式相依套件由 Gradle 下載，版本固定於 `build.gradle.kts`：Kotlin、Compose Multiplatform / Material 3、kotlinx.coroutines、OkHttp、org.json、JNA / JNA Platform、CommonMark Java、PDFBox、ICU4J 和 OpenJFX。測試相依套件還包含 JUnit、MockWebServer 和 Mockito。各元件保留自己的上游授權與散布聲明。
- `gradlew`、`gradlew.bat` 和 Gradle Wrapper 來自原專案，使用 Gradle 8.13。

建置正式二進位發行版時，應隨發行套件保留相依套件內附的授權與聲明；原始碼套件不包含相依套件快取。配套可攜版包含執行所需的相依 JAR，保留其內嵌聲明，並在 `licenses/dependencies` 下另存可識別的授權與聲明文字。

- Windows 可攜版包含未修改的 Eclipse Temurin JRE 21.0.12.1+1 x64：[官方發行版](https://github.com/adoptium/temurin21-binaries/releases/tag/jdk-21.0.12.1%2B1)。執行環境的完整 `legal` 目錄與 `NOTICE` 一併保留。OpenJDK 原始碼與建置來源由 `runtime/release` 中的上游連結記錄；授權為各模組內附的 GPLv2 with Classpath Exception 等聲明。
- OpenJFX 使用官方 21.0.8 Windows JAR：[OpenJFX 原始碼與授權](https://github.com/openjdk/jfx)。Skiko 使用 `skiko-awt-runtime-windows-x64` 0.9.37.4。未將 Linux 原生函式庫重新命名為 Windows 原生函式庫。
- 打包檔案的版本、大小與校驗摘要記錄在可攜版的 `manifest.json`。

## Fluent System Icons

介面圖示使用 Microsoft Fluent System Icons 中未修改的 SVG 資產，npm 套件為 `@fluentui/svg-icons` 1.1.341。MIT 授權全文：`licenses/Fluent-System-Icons-LICENSE.txt`。來源對照與每個資產的 SHA-256 記錄於 `docs/fluent-icons.json`。

來源：https://github.com/microsoft/fluentui-system-icons

## NSIS 安裝程式

Windows 安裝程式與小型啟動器使用 NSIS 3.x 編譯。NSIS 核心使用 zlib/libpng 授權，詳見 https://nsis.sourceforge.io/License 。應用程式不包含 NSIS 建置工具。

## 1.6.0 文件預覽

使用 Apache POI 5.5.1（poi-ooxml 與 poi-scratchpad）、Apache PDFBox 3.0.8、jsoup 1.23.2，以及 CommonMark Java 0.24.0 GFM 刪除線擴充套件。打包的 JAR 相依套件之上游 LICENSE／NOTICE 檔案保留於 `licenses/dependencies`；版本與雜湊值記錄於可攜版資訊清單。

## Desktop 2.0.0

首頁協定、卡片解析與互動、操作回執、writer、連線心跳及語音文字拆分適配自使用者提供的 Android 4.0.0 發行版原始碼。保留原協定版本與來源說明。

本機語音使用 sherpa-onnx v1.13.5 的 Java API 與對應 Windows x64／macOS arm64 原生函式庫，Apache-2.0 授權保存在 `licenses/sherpa-onnx-LICENSE.txt`。上游：https://github.com/k2-fsa/sherpa-onnx 。相依函式庫的內嵌授權隨 JAR 保留。

SenseVoice int8 與 Kokoro multilingual v1.1 int8 模型由使用者按需從 sherpa-onnx 官方 GitHub Release 下載，應用程式安裝套件不包含模型。模型版本、網址、完整 SHA-256 與解壓縮要求見 `LocalVoiceModels.kt`；模型各自的授權隨下載封存檔保留。Apache Commons Compress 用於限制範圍的解壓縮。

Windows 2.0.0 執行環境由通過發行者 SHA-256 校驗的 Temurin JDK 21.0.12.1+1 連結產生；Mac 驗收套件沿用使用者 1.9.0 發行套件內的 Apple Silicon 啟動器、Java 執行環境與系統語音 helper，替換全部應用程式 JAR 後重新簽章。建置資訊清單保留各元件摘要。

第三方授權檔案與原始驗證資料保留原文；本頁僅翻譯專案的來源說明。
