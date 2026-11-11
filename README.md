# 家豪的交界地戰術資料庫（Lands Between Tactical Wiki）

> **TAICA 生成式 AI：文字與圖像生成的原理與實務｜Week 09 作業：建立一個自己的 AGENTS.md**  
> **學生**：中央大學 電機二A 林鑫吾（11450101010）

本專案是一個以 **Agentic Work（AI Agent = AI Model + Harness）** 核心理念打造的《艾爾登法環（Elden Ring）》戰術與數據知識庫網站。  
透過根目錄的 [AGENTS.md](./AGENTS.md)（AI 員工手冊／專案憲法），定義了明確的**視覺色票、目錄結構、內容先行工作流（
otes/<slug>.md → guides/<slug>/index.html）與擴充規範**，讓 AI 能隨時依照同一套標準快速新增攻略頁面。

## 📂 專案結構

`	ext
elden-ring-wiki/
├── index.html                                  # 知識庫總目錄首頁（含即時搜尋與分類篩選）
├── AGENTS.md                                   # AI 員工手冊（專案憲法：定義風格、結構与擴充 SOP）
├── NOTES.md                                    # 現況白板與待辦事項（每次工作結束前由 AI 更新）
├── log.md                                      # 決策與架構變更紀錄（只增不刪）
├── .nojekyll                                   # GitHub Pages 純靜態站設定檔
├── notes/                                      # 【內容先行】各篇攻略的 Markdown 數據內容稿
│   ├── malenia-blade-of-miquella.md
│   ├── moonveil-katana-build.md
│   └── equip-load-calculator.md
└── guides/                                     # 【實際網頁成品】每篇攻略獨立一個英文 slug 資料夾
    ├── malenia-blade-of-miquella/
    │   └── index.html                          # 頭目攻略：女武神瑪蓮妮亞（含水鳥亂舞斷招模擬）
    ├── moonveil-katana-build/
    │   └── index.html                          # 流派配裝：名刀月隱智力居合流（含削韌與配點試算）
    └── equip-load-calculator/
        └── index.html                          # 互動工具：交界地圓桌補給站＆翻滾負重即時計算機
`
