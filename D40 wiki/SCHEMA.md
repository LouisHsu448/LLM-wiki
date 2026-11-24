# LLM Wiki 系統規範與操作協定 (SCHEMA)

> **基於 Andrej Karpathy LLM Wiki 模式**  
> *「Wiki 是持續生長、複合累積的知識庫；筆記軟體/瀏覽工具是 IDE，LLM 是工程師，Wiki 是被維護的原始程式碼。」*

---

## 1. 核心哲學與系統目的

傳統 RAG（檢索增強生成）在每次使用者提問時，僅從原始檔案切塊拼湊回答，缺乏跨會話的知識沈澱與提煉。
本 **D40 攝影入門 LLM Wiki** 是一個主動複合、具備結構化記憶的知識系統：
1. **原始筆記 (`raw/notes/`)**：作為不可變真實來源（Immutable Source of Truth），嚴禁由系統任意修改。
2. **Wiki 詞條 (`wiki/`)**：由 LLM 消化、提煉並結構化維護的知識網絡，分為光學理論 (`concepts/`)、相機硬體操作 (`hardware/`) 與實戰決策流程 (`workflows/`)。
3. **複合演進 (Compounding)**：每一篇新材料的加入，都會穿透、更新與補強多個相關詞條，保持整體知識庫的互聯性與一致性。
4. **雙向連結 (`[[Wikilink]]`)**：所有關鍵概念、硬體部件與操作流程皆透過雙向連結織成知識圖譜，徹底消除孤島頁面。

---

## 2. 目錄階層架構

```text
.
├── raw/
│   └── notes/                     # 唯讀原始素材（使用者提供）
│       ├── 01_exposure_triangle.md
│       ├── 02_nikon_d40_controls.md
│       ├── 03_metering_and_histogram.md
│       ├── 04_lens_focal_length.md
│       └── 05_raw_vs_jpeg_post.md
│
├── wiki/                          # LLM 維護之知識核心
│   ├── concepts/                  # 核心光學與攝影理論
│   │   ├── 曝光三角.md
│   │   ├── 光圈與景深.md
│   │   ├── 快門速度與動態表現.md
│   │   ├── 感光度與噪點控制.md
│   │   ├── 測光模式與18灰.md
│   │   ├── 曝光補償.md
│   │   ├── 直方圖與高光警告.md
│   │   ├── 片幅裁切與等效焦距.md
│   │   ├── 安全快門法則.md
│   │   └── RAW與色彩動態範圍.md
│   │
│   ├── hardware/                  # Nikon D40 硬體與鏡頭系統
│   │   ├── Nikon_D40_機身特點.md
│   │   ├── D40_按鍵與指令滾輪操作.md
│   │   ├── D40_曝光模式詳解.md
│   │   ├── D40_對焦馬達限制與鏡頭選購.md
│   │   └── Nikkor_18-55mm_Kit鏡解析.md
│   │
│   └── workflows/                 # 實戰操作流程與場景處方簽（Synthesis 層）
│       ├── 新手第一天戶外實拍流程.md
│       ├── 室內與微光拍攝處方簽.md
│       ├── 人像散景最大化攻略.md
│       └── 逆光與大光比曝光決策.md
│
├── index.md                       # 知識目錄索引（包含單行濃縮精華）
├── log.md                         # 系統運作日誌（記錄 Ingest、Refactor、Lint 軌跡）
└── SCHEMA.md                      # 本規範定義文件
```

---

## 3. 詞條標準結構規範

所有在 `wiki/` 目錄下的文件，均須嚴格遵守以下結構與 Frontmatter 定義：

### 3.1 YAML Frontmatter 格式
```yaml
---
title: "詞條完整標題"
category: "concept | hardware | workflow"
tags:
  - "photography/領域標籤"
  - "nikon-d40/硬體標籤"
difficulty: "Beginner | Intermediate"
created: YYYY-MM-DD
updated: YYYY-MM-DD
prerequisites:
  - "[[必讀前置詞條]]"
related_topics:
  - "[[關聯詞條]]"
---
```

### 3.2 內文必備 5 大區塊
1. **💡 30秒白話精華（TL;DR）**：無技術門檻的白話核心定義。
2. **🎯 核心原理與物理機制**：光學/電子物理原理解析，必備數學公式或比喻。
3. **📷 Nikon D40 專屬實操與硬體映射**：實體按鍵、轉盤滾輪操作、觀景窗與 LCD 顯示符號。
4. **⚠️ 新手最常踩的坑與除錯表**：條列易搞混盲區與排錯對照表。
5. **🔗 相關知識網絡**：列出前置詞條、延伸主題與雙向連結。

---

## 4. 雙向連結語法與連結維護規範

1. **語法標準**：統一採用 `[[頁面名稱]]` 或 `[[頁面名稱|顯示別名]]`。
2. **入鏈與出鏈**：除 `index.md` 外，每個 Wiki 詞條至少具備 2 個入鏈與 2 個出鏈。
3. **禁止斷鏈與孤島**：所有雙向連結引用的目標頁面必須真實存在，不可指向無效檔案。
