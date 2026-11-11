# AGENTS.md — 家豪的交界地戰術資料庫（Lands Between Tactical Wiki）專案指引

> 這份檔案（`AGENTS.md`）是給 AI Agent 與人類協作者看的「專案憲法（員工手冊）」。  
> **動手做任何事之前，請先完整閱讀本檔**，再讀 `NOTES.md`（目前進度、下次從哪開始、待辦清單）與 `log.md`（近期會影響決策的架構變更）。  
> 任何新增或修改頁面的任務，都必須嚴格遵守本文件的規範；**每次工作結束前請同步更新 `NOTES.md`**。

---

## 一、這個專案的目的（我們在做什麼）

本專案是**「家豪的交界地戰術資料庫（Lands Between Tactical Wiki）」**——一個專為《艾爾登法環（Elden Ring）》玩家打造的**結構化戰術數據與配裝知識庫網站**。

- **專案核心精神**：解決一般遊戲攻略網「文字雜亂、缺乏精確數據（如韌性值、異常狀態抗性、負重門檻）」的痛點，所有攻略一律以**結構化數據卡片 + 互動式試算小工具**呈現。
- **敘事人設（家豪語氣）**：站長「家豪」是一名身穿全黑重磅連帽衛衣、臉戴 3D 黑色口罩、耳機單邊播放 Alan Walker 電音的**《艾爾登法環》資深數據流黑客玩家**。
  - 每個頁面的頂部或戰術點評區，固定包含一個 **「🎧 家豪的終端機戰術點評」** 區塊，帶有一點中二裝酷但極度務實講求數據的口吻（例如：「（推了一下黑口罩）呵，連女武神的水鳥亂舞幀數都沒摸透就敢進霧門？看清楚下面的凍傷閾值數據…」）。
  - 其餘數據表格、配裝清單與機制解析則保持**客觀、精確、條理分明**。
- **技術型態**：純靜態 **HTML5 + CSS3 + 原生 JavaScript（Vanilla JS）**，無須後端伺服器或打包工具（No build step），直接部署於 **GitHub Pages**。

---

## 二、資料夾結構與檔案命名規則

> **本資料夾即為 GitHub Repository 根目錄**。為了確保 GitHub Pages 網址乾淨且不產生編碼問題，**所有出現在 URL 的資料夾與檔案名稱一律使用「英文小寫 + 連字號（kebab-case slug）」**，嚴禁使用中文檔名或空格。

```text
elden-ring-wiki/                        （= GitHub repo 根目錄 / GitHub Pages 根目錄）
├── index.html                          ← 知識庫總目錄首頁（含關鍵字即時搜尋、分類篩選、所有攻略卡片）
├── AGENTS.md                           ← 本檔（AI 員工手冊／專案開發憲法）
├── NOTES.md                            ← 現況白板（目前完成頁面、待辦清單、下次接手進度）
├── log.md                              ← 變更紀錄（只記會改變未來決策的規範調整，只增不刪）
├── README.md                           ← GitHub Repo 專案說明頁
├── .nojekyll                           ← 讓 GitHub Pages 不跑 Jekyll 的標記檔
├── notes/                              ← 【內容先行】各篇攻略的 Markdown 原始數據稿（notes/<slug>.md）
│   ├── malenia-blade-of-miquella.md    ← 女武神瑪蓮妮亞數據稿
│   ├── moonveil-katana-build.md        ← 名刀月隱智力居合流數據稿
│   └── equip-load-calculator.md        ← 圓桌補給站與裝備負重試算規格稿
└── guides/                             ← 【實際網頁成品】每篇攻略一個英文 slug 子資料夾
    ├── malenia-blade-of-miquella/
    │   └── index.html                  ← 單篇攻略完整網頁（self-contained）
    ├── moonveil-katana-build/
    │   └── index.html
    └── equip-load-calculator/
        └── index.html
```

### 命名一致性鐵則
每一篇攻略主題都對應唯一一個英文 `<slug>`（例如新增鮮血君王蒙格攻略，slug 定為 `mohg-lord-of-blood`），且在以下三個位置必須完全一致：
1. **內容稿路徑**：`notes/<slug>.md`（如 `notes/mohg-lord-of-blood.md`）
2. **網頁成品路徑**：`guides/<slug>/index.html`（如 `guides/mohg-lord-of-blood/index.html`）
3. **首頁卡片連結**：根目錄 `index.html` 中的 `<a class="guide-card" href="guides/<slug>/">`

---

## 三、網頁整體風格與品牌視覺規範（切勿自行更改）

所有頁面（包含首頁 `index.html` 與各篇 `guides/<slug>/index.html`）必須共用同一套**「交界地黑金 × 家豪終端機電音藍」深色科技奇幻主題**。

### 1. 標準色票（CSS Variables）
任何新頁面的 `<style>` 根部必須宣告並使用以下 CSS 變數：
```css
:root {
  --bg-deep: #0b0e14;        /* 終端機底層深黑 */
  --bg-card: #131822;        /* 戰術資料卡片底色 */
  --bg-card-hover: #1a2230;  /* 卡片懸停底色 */
  --gold: #d4af37;           /* 黃金律法主色（主標題、重要外框、高光） */
  --gold-soft: rgba(212, 175, 55, 0.16); /* 黃金半透明標籤底色 */
  --cyan: #38bdf8;           /* 家豪終端機電音藍（數據指標、互動按鈕、程式碼） */
  --cyan-soft: rgba(56, 189, 248, 0.14);
  --crimson: #f43f5e;        /* 猩紅腐敗／危險警告／出血弱點標記 */
  --emerald: #10b981;        /* 安全通過／輕中負重合格／高抗性標記 */
  --text-main: #e2e8f0;      /* 主要內文亮灰白 */
  --text-muted: #94a3b8;     /* 次要說明灰藍 */
  --border: #263042;         /* 卡片基礎邊框 */
}
```

### 2. 字體與排版規範
- **字體載入**：Google Fonts 的 `Noto Sans TC`（中文與一般內文）搭配 `JetBrains Mono`（數值、百分比、終端機代號、公式）。
- **標點符號**：中文內文一律使用**全形標點符號**（，。、：「」！？（）），數值與單位之間保留半形空格或直接連寫（如 `80 韌性`、`70.0%`）。
- **響應式設計（RWD）**：容器最大寬度 `max-width: 1020px`，手機螢幕（`@media (max-width: 680px)`）下雙欄網格自動轉為單欄直排，禁止出現整頁橫向捲軸。

---

## 四、頁面結構與三種內容模版

本知識庫將所有頁面分為 **3 大戰術分類（Categories）**，動工前必須先確認新頁面屬於哪一類：

### 類別 A：`BOSS 戰術解析`（頭目攻略頁）
適用於交界地與幽影之地各個主線／追憶頭目（如 `malenia-blade-of-miquella`）。頁面必須由上而下包含以下 5 個標準區塊：
1. **頂部導覽列（Top Nav）**：返回總目錄首頁連結（`../../index.html`）＋ 檔案編號徽章（如 `[FILE_001]`）。
2. **頭目標題與家豪終端機點評（Hero + Jiahao Terminal Quote）**：頭目中英文名稱、所在區域、家豪的毒舌戰術摘要。
3. **核心數據儀表板（Boss Stats Grid）**：4 張數據小卡（一／二階段 HP、韌性值 Poise、パリィ／處決需求、推薦等級與骨灰）。
4. **屬性吸收率與異常狀態閾值表（Weakness & Status Table）**：清楚標示「弱點（如凍傷、出血）」與「免疫／高抗（如腐敗、聖屬性）」。
5. **關鍵殺招拆解與互動模擬器（Interactive Mechanics Widget）**：拆解最具威脅的招式（如水鳥亂舞三連斬），並附帶一個原生 JS 互動小工具（如「冰凍壺斷招／削韌計算器」或「階段切換策略」）。

### 類別 B：`流派與武器配裝`（Build 指南頁）
適用於熱門武器與流派配置（如 `moonveil-katana-build`）。頁面必須包含：
1. **頂部導覽列** ＋ **武器標題與家豪終端機點評**。
2. **武器基礎規格卡（Weapon Spec Grid）**：取得位置、能力值需求（力／敏／智／信／感）、補正等級、專屬戰技名稱與 FP 消耗。
3. **戰技削韌與傷害數據表（Stance Damage Table）**：列出輕擊、重擊戰技的削韌值與實戰連段。
4. **畢業護符、靈藥與防具搭配清單（Loadout Cards）**：推薦的 4 個護符與靈藥露滴組合。
5. **互動式配點／傷害試算器（Interactive Build Calculator）**：讓玩家調整等級或智力／敏捷配點，即時預覽建議屬性分配。

### 類別 C：`戰術試算工具`（Interactive Utility 頁）
適用於跨流派通用計算機（如 `equip-load-calculator` 圓桌補給站與裝備負重計算機）。頁面必須包含：
1. **頂部導覽列** ＋ **工具標題與家豪終端機點評**。
2. **即時互動輸入面板（Interactive Form / Sliders）**：使用原生 JS 綁定 `input` 或 `click` 事件，不依賴外部框架，狀態保存在記憶體變數中。
3. **判定標準對照表（Reference Rules Table）**：列出計算公式與門檻（例如 `< 30%` 輕負重、`< 70%` 中負重、`>= 70%` 重負重肥滾）。

---

## 五、標準作業流程（SOP）：新增內容時要遵守的步驟

> **⚠️ 鐵則：內容先行（Content First）。**  
> 當使用者要求「幫我新增一篇 XXX 的頁面／攻略」時，AI **絕對不可以只改一個檔案**，必須依序完成以下 **4 個標準步驟**：

### Step 1：先建立 `notes/<slug>.md` 數據內容稿
在 `notes/` 資料夾下建立 `<slug>.md`，開頭必須包含以下 Metadata 標頭格式，並整理好所有真實數據（不得捏造不存在的護符或錯誤數值）：
```markdown
# [標題名稱]
- **Slug**: `<slug>`
- **分類**: `BOSS 戰術解析` | `流派與武器配裝` | `戰術試算工具`
- **檔案編號**: `DOC_00X`
- **難度或評級**: `★★★★★` 或 `S 級主流`
- **成品路徑**: `guides/<slug>/index.html`
- **狀態**: ✅ 已定稿並生成網頁
```

### Step 2：建立 `guides/<slug>/index.html` 獨立網頁
- 依循第三節的 CSS 色票與第四節對應類別（A / B / C）的 5 大區塊結構，產出完整、可獨立開啟（Self-contained）的 `guides/<slug>/index.html`。
- 確保頂部「← 返回交界地戰術總目錄」連結指向 `../../index.html`。
- 確保頁面底部包含統一的「其他戰術檔案快速跳轉」連結與頁尾版權宣告。

### Step 3：將新頁面註冊進首頁 `index.html`
打開根目錄的 `index.html`，在「戰術檔案庫（Guide Cards Grid）」區塊中，依照以下標準卡片 HTML 結構新增一張卡片（注意 `data-category` 與 `data-keywords` 必須填寫，以支援首頁的即時搜尋與分類篩選功能）：
```html
<a class="guide-card" href="guides/<slug>/" data-category="boss|build|tool" data-keywords="關鍵字1 關鍵字2">
  <div class="card-top">
    <span class="file-id">[DOC_00X]</span>
    <span class="badge badge-boss">分類標籤</span>
  </div>
  <h3>頁面主標題</h3>
  <p>一句話到兩句話的戰術核心摘要，說明這頁解決什麼問題與包含什麼互動工具。</p>
  <div class="tags">
    <span class="tag">#標籤1</span>
    <span class="tag">#標籤2</span>
    <span class="tag">#標籤3</span>
  </div>
  <span class="card-cta">調閱終端機檔案 →</span>
</a>
```
同時更新首頁頂部儀表板的「已收錄戰術檔案數」統計數字。

### Step 4：更新 `NOTES.md` 與 `log.md`
- 在 `NOTES.md` 的「已完成頁面清單」補上新頁面，並更新待辦事項。
- 若有新增分類、修改色票或新增元件規範，在 `log.md` 新增一筆日期紀錄。

---

## 六、給 AI 的嚴格限制與檢查清單（Do's & Don'ts）

1. **禁止破壞既有結構**：修改或新增頁面時，不可刪除首頁既有的攻略卡片，也不可移除 CSS `:root` 色票變數。
2. **禁止捏造遊戲數據**：《艾爾登法環》的關鍵門檻（例如中翻滾負重上限為 `70.0%`、輕翻滾為 `30.0%`、名刀月隱智力需求為 `23`、女武神一階段韌性為 `80`）必須準確無誤。若不確定某個冷門數值，請標註「依當前版本實測約…」或向使用者確認。
3. **Self-Contained 無外部依賴**：除了 Google Fonts 字體外，所有圖示一律使用內嵌 SVG 或 Emoji，所有樣式與互動腳本一律內嵌於該頁的 `index.html`，確保上傳 GitHub Pages 後 **100% 不破圖、不報錯（Zero 404）**。
4. **保持「家豪」人設溫度**：每頁的「🎧 家豪的終端機戰術點評」都要符合「穿黑衛衣、推黑口罩、聽電音、講話微中二但數據超專業」的特色，讓整個網站具有一致的個人品牌識別度。
