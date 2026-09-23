# NTUT SSO Lab 網站

陳威丞老師實驗室網站。純靜態網頁，不需要資料庫或後端。

```
SSOLab_Website/
├── index.html     ← 整個網站（內容、版型、程式都在這一個檔）
├── img/           ← 所有圖片
├── .nojekyll      ← GitHub Pages 需要，不要刪
└── README.md      ← 這份說明
```

---

## 一、怎麼更新成員名單

用**記事本**或 **VS Code** 打開 `index.html`，按 `Ctrl+F` 搜尋 `var MEMBERS`。
你會看到這一段，照格式改就好，版面會自動排：

```js
{ key:"master", group:"Master's Students", zh:"碩士班研究生", people:[
    { name:"傅冠綸", nick:"Alston" },
    { name:"陳聖昀", nick:"Teddy" },
    { name:"吳昀臻", nick:"" },          // 沒有暱稱就留空字串
    { name:"鄧杰平", nick:"JP" },
    { name:"馮俊維", nick:"小馮" }
]},
```

- **新增一位**：複製一行 `{ name:"○○○", nick:"○○" },` 貼在下面，改成新名字
- **刪除一位**：整行刪掉
- **某個學制沒人**：把 `people:[]` 留空，那一組會自動從頁面上消失
- 每一行結尾的**逗號不要漏**，最後一行可以不用

### 要放照片的話

```js
{ name:"傅冠綸", nick:"Alston", photo:"img/member_alston.jpg" },
```

把照片放進 `img/` 資料夾，`photo` 填相對路徑。不填就自動用姓名末兩字生成圓形頭像。

---

## 二、怎麼更新畢業生

搜尋 `var ALUMNI`，目前是空的 `[]`。有畢業生之後這樣填：

```js
var ALUMNI = [
  { name:"王小明", degree:"M.S.", thesis:"鈣鈦礦量子點光偵測器", year:"2028", now:"台積電" },
];
```

填了之後 Alumni 頁的表格會自動出現。

---

## 三、怎麼更新論文

搜尋 `var PUBS`。每一筆的格式：

```js
{ y:2026, a:"作者群", t:"論文標題", v:"Journal Abbrev.", d:"2026, 卷, 頁", f:"10.7", first:true },
```

- `y` 年份（決定分在哪一區，年份篩選按鈕會自動增加）
- `a` 作者、`t` 標題、`v` 期刊、`d` 卷期頁
- `f` impact factor，不想顯示就填 `""`
- `first:true` 會標上 FIRST AUTHOR；共同第一作者用 `co:true`

---

## 四、怎麼更新 Lab News

搜尋 `Lab News`，在 HTML 裡直接改，照現有格式複製一段：

```html
<div class="news-item">
  <time datetime="2026-09-01">Sep 1, 2026</time>
  <p><span class="kind">Milestone</span>這裡寫內容。</p>
</div>
```

`kind` 那格是標籤文字，可以自己寫（Milestone / People / Conference / Invited talk / Award…）。

---

## 五、怎麼上線

### 方法 A：Netlify（最快，兩分鐘，不用裝任何東西）

1. 開 https://app.netlify.com/drop
2. 把整個 `SSOLab_Website` 資料夾拖進去
3. 馬上會給你一個網址，例如 `random-name-123.netlify.app`
4. 註冊免費帳號後可以改成 `ntutssolab.netlify.app`，也可以綁自訂網域

之後要更新，重新拖一次資料夾就好。

### 方法 B：GitHub Pages（適合長期維護，有版本紀錄）

1. 在 GitHub 建一個 repository，例如 `ntut-sso-lab`
2. 把資料夾裡的檔案全部上傳（網頁介面可以直接拖曳）
3. Settings → Pages → Source 選 `main` 分支、根目錄 `/`
4. 網址會是 `https://<帳號>.github.io/ntut-sso-lab/`

**綁系上或自訂網域**：兩個平台都支援。GitHub Pages 是在 repo 根目錄放一個 `CNAME` 檔，
裡面寫你的網域；Netlify 則在後台 Domain settings 設定。DNS 那邊要請網域管理者加一筆記錄。

---

## 六、注意事項

- **字型**來自 Google Fonts（Newsreader、Source Sans 3），需要連網才會正確顯示
- **深淺色**跟隨訪客系統設定自動切換，右上角也可以手動切
- **圖片**請先壓到寬度 1200–1600px 再放進 `img/`，避免拖慢載入
- 改完 `index.html` 後，**先在本機用瀏覽器打開確認沒問題**，再上傳
- 這份網站的原始設計稿與所有原始圖片備份，另存在 `桌面\SSOLab_網站圖片`
