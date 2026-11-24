# LLM Wiki 系統運作與變更日誌 (Operational Log)

本文件依據 Karpathy LLM Wiki 模式建立，作為不可篡改的系統操作日誌（Append-only Audit Trail），精確追蹤知識庫的每次匯入 (Ingest)、重構 (Refactor)、合成 (Synthesize) 與健康檢查 (Lint)。

---

## [2026-11-24] init & ingest | 初始知識庫建構與 5 篇原始資料消化

### 1. 觸發事件
使用者依據 Andrej Karpathy 的 LLM Wiki 模式，委託在工作區建立「數位單眼攝影與曝光三角入門（以 Nikon D40 為例）」知識庫，並提供 5 篇核心原始筆記。

### 2. 原始檔案封存 (`raw/notes/`)
已建立唯讀不可變原始資料源：
- `raw/notes/01_exposure_triangle.md`
- `raw/notes/02_nikon_d40_controls.md`
- `raw/notes/03_metering_and_histogram.md`
- `raw/notes/04_lens_focal_length.md`
- `raw/notes/05_raw_vs_jpeg_post.md`

### 3. 系統協定建立
- `SCHEMA.md`：定義目錄規範、知識分層（Concepts / Hardware / Workflows）、YAML Frontmatter 結構與雙向連結維護協定。

### 4. 複合提煉生成之 Wiki 詞條 (共 19 個核心文件)

#### A. 核心光學與理論詞條 (`wiki/concepts/`)
- `曝光三角.md`：消化 01 筆記，建立互易律與能量守恆數學關係式。
- `光圈與景深.md`：解構 f 倒數物理意義與景深三大控制變數。
- `快門速度與動態表現.md`：凍結動作與動態模糊之時間控制。
- `感光度與噪點控制.md`：解析類比增益、D40 原生 ISO 200 與 CCD 抗噪極限。
- `測光模式與18灰.md`：消化 03 筆記，剖析 18% 中性灰大腦與三種測光模式。
- `曝光補償.md`：解析半自動與手動模式下的本質差異，確立白加黑減原則。
- `直方圖與高光警告.md`：斷層削波 (Clipping) 危害、向右曝光 (ETTR) 與 Blinkies 判定。
- `片幅裁切與等效焦距.md`：消化 04 筆記，定義 APS-C 1.5x 裁切與視角換算。
- `安全快門法則.md`：手持防震倒數法則在 APS-C 上的 1.5x 修正計算。
- `RAW與色彩動態範圍.md`：消化 05 筆記，比較 12-bit NEF 與 8-bit JPEG、Lightroom 5 步調色。

#### B. Nikon D40 機身與鏡頭實體詞條 (`wiki/hardware/`)
- `Nikon_D40_機身特點.md`：整合 6.1MP CCD 發色、1/500s 混合快門閃燈同步硬體優勢。
- `D40_按鍵與指令滾輪操作.md`：消化 02 筆記，建立單滾輪 + `[+/-]` 複合鍵與 `[i]` 選單速查表。
- `D40_曝光模式詳解.md`：P/S/A/M 各模式調控行為與觀景窗電子類比曝光尺規解析。
- `D40_對焦馬達限制與鏡頭選購.md`：深入拆解機身無馬達限制，建立 AF-S / AF-D 相容矩陣與避坑清單。
- `Nikkor_18-55mm_Kit鏡解析.md`：拆解隨機 Kit 鏡之浮動光圈、28cm 近拍能力與 f/8 甜區。

#### C. 新手實戰操作流程詞條 (`wiki/workflows/`)
- `新手第一天戶外實拍流程.md`：整合出門前檢查 $\rightarrow$ A 模式實操 $\rightarrow$ 直方圖複查之標準作業流程。
- `室內與微光拍攝處方簽.md`：針對 Kit 鏡小光圈與 CCD 高感短板，擬定廣角端全開、ISO 800、安全快門與慢速同步閃光策略。
- `人像散景最大化攻略.md`：推導 18-55mm Kit 鏡在 55mm f/5.6 端最大化散景之「焦段、人距、景距」黃金比例。
- `逆光與大光比曝光決策.md`：分析剪影風格、日系高調人像，並啟動 D40 1/500s 高速壓光神技。

#### D. 知識目錄 (`index.md`)
- 彙整全系統主題索引，為每個詞條提供 1 行濃縮核心洞察（Core Insight）。

---

## 狀態審計總結
- **檔案完整性**：100%（22 個文件全部建置完畢）
- **雙向連結網絡**：全詞條均具備雙向交叉引用，無孤島文件
- **健康狀態**：正常 (Healthy)


---

## [2026-11-24] generate | 建立單一檔案教學型 HTML 簡報 (presentation.html) 與完整性審查

### 1. 觸發事件
使用者請求依據 `wiki/` 核心知識內容，在專案根目錄生成一份零外部依賴、單一檔案的教學型互動 HTML 簡報（`presentation.html`），針對完全零基礎單眼新手進行教學。

### 2. 生成檔案與規格
- **檔案路徑**：`presentation.html`（專案根目錄，大小約 75 KB）
- **技術架構**：
  - 單一檔案（Single-file HTML5），內嵌純原生 CSS 與 JavaScript，零外部網路依賴，完全支援離線播放。
  - 響應式佈局（Desktop / Tablet / Mobile 自適應），支援深色相機質感主題與現代排版。
  - 鍵盤控制：支援 `ArrowLeft` / `ArrowRight`、`Space`、`Enter`、`Home`、`End`、`F`（全螢幕切換）、`M`（章節導航選單）。
  - 觸控支援：支援行動裝置左右滑動（Touch Swipe）換頁。
  - 頂部平滑進度條 + 底部導航欄（頁碼計數、下拉選單跳頁、全螢幕按鈕）。
- **投影片結構（共 23 頁）**：
  - Slide 1: 封面與簡報導覽（來源：`index.md & SCHEMA.md`）
  - Slide 2: 什麼是數位單眼？光學反光鏡與感光元件（來源：`wiki/hardware/Nikon_D40_機身特點.md`）
  - Slide 3: 核心概念 01：曝光的物理本質（水桶裝水比喻）（來源：`wiki/concepts/曝光三角.md`）
  - Slide 4: 核心概念 02：光圈與景深（瞳孔與倒數之謎）（來源：`wiki/concepts/光圈與景深.md`）
  - Slide 5: 核心概念 03：快門速度與動態表現（冰凍時間 vs 流水絹絲）（來源：`wiki/concepts/快門速度與動態表現.md`）
  - Slide 6: 核心概念 04：感光度與噪點控制（訊號放大鏡與 CCD 特性）（來源：`wiki/concepts/感光度與噪點控制.md`）
  - Slide 7: 核心概念 05：曝光三角互易律實戰（一加一減的平衡術）（來源：`wiki/concepts/曝光三角.md`）
  - Slide 8: 核心概念 06：測光模式與 18% 中性灰（相機大腦是個色盲）（來源：`wiki/concepts/測光模式與18灰.md`）
  - Slide 9: 核心概念 07：曝光補償的「白加黑減」心法（來源：`wiki/concepts/曝光補償.md`）
  - Slide 10: 核心概念 08：直方圖與高光警告（拒絕被 2.5 吋螢幕欺騙）（來源：`wiki/concepts/直方圖與高光警告.md`）
  - Slide 11: 核心概念 09：APS-C 片幅裁切與等效焦距（1.5x 視角放大鏡）（來源：`wiki/concepts/片幅裁切與等效焦距.md`）
  - Slide 12: 核心概念 10：安全快門法則（手持不糊片的速度底線）（來源：`wiki/concepts/安全快門法則.md`）
  - Slide 13: 核心概念 11：RAW (NEF) vs JPEG（生鮮食材 vs 熟食便當）（來源：`wiki/concepts/RAW與色彩動態範圍.md`）
  - Slide 14: 硬體解構 01：Nikon D40 傳奇特色（CCD 發色與 1/500s 閃燈同步）（來源：`wiki/hardware/Nikon_D40_機身特點.md`）
  - Slide 15: 硬體解構 02：D40 單指令滾輪操控流（單手按住 [+/-] 雙用滾輪）（來源：`wiki/hardware/D40_按鍵與指令滾輪操作.md`）
  - Slide 16: 硬體解構 03：D40 曝光模式詳解（告別 AUTO，擁抱 A 模式）（來源：`wiki/hardware/D40_曝光模式詳解.md`）
  - Slide 17: 硬體解構 04：D40 購鏡避坑指南：機身無對焦馬達死穴（來源：`wiki/hardware/D40_對焦馬達限制與鏡頭選購.md`）
  - Slide 18: 硬體解構 05：隨機 Kit 鏡潛力榨取（18-55mm 浮動光圈與近拍）（來源：`wiki/hardware/Nikkor_18-55mm_Kit鏡解析.md`）
  - Slide 19: 實戰流程 01：新手第一天戶外實拍 SOP（出發 → 拍攝 → 複查）（來源：`wiki/workflows/新手第一天戶外實拍流程.md`）
  - Slide 20: 實戰流程 02：Kit 鏡人像散景最大化攻略：焦段、人距、景距（來源：`wiki/workflows/人像散景最大化攻略.md`）
  - Slide 21: 實戰流程 03：室內微光拍攝極限處方簽：18mm 全開、ISO 800（來源：`wiki/workflows/室內與微光拍攝處方簽.md`）
  - Slide 22: 實戰流程 04：逆光與大光比曝光決策：剪影 vs 日系過曝 vs 壓光（來源：`wiki/workflows/逆光與大光比曝光決策.md`）
  - Slide 23: 總結與展望：邁向手動掌控光影的攝影師之路（來源：`index.md & 全系列 19 篇詞條`）

### 3. 審計與健康檢查結果
- **內容忠實性審查**：100% 嚴格忠於 `wiki/` 內容，參數、按鍵操作、比喻與光學公式均與知識庫一致，無額外捏造。
- **來源標註審查**：23 / 23 頁投影片全數標記來源詞條徽章。
- **健康狀態**：正常 (Healthy)
