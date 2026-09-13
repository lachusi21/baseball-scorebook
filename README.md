# 棒球記分本

一頁式靜態網站：寫給小學四年級學生看的棒球統計課。從「為什麼棒球天生適合統計」講到
OPS、wOBA、wRC+ 與 Statcast 進階數據，全部配 2026 年 MLB 真實數據，最後附大谷翔平的球員卡。

資料截至 **2026-09-13**，來源為 [Baseball Savant](https://baseballsavant.mlb.com/)
原始資料檔（242 位合格打者，百分位為自行計算）與 [StatMuse](https://www.statmuse.com/mlb)。

## 結構

```
public/index.html   ← 網站本體，單一檔案，無建置步驟、無相依套件
public/.nojekyll    ← 讓 GitHub Pages 直接吐靜態檔，不要跑 Jekyll
.github/workflows/  ← 兩條自動部署流程
```

外部資源只有 Google Fonts（Noto Sans SC / Noto Serif SC / Oswald）。
其餘 CSS、SVG 圖都內嵌在 `index.html` 裡。

## 部署

推到 `main` 會同時觸發兩條流程：

| 流程 | 檔案 | 需要的設定 |
|---|---|---|
| GitHub Pages | `pages.yml` | Settings → Pages → Source 選 **GitHub Actions** |
| Cloudflare Pages | `cloudflare.yml` | repo secrets：`CLOUDFLARE_API_TOKEN`、`CLOUDFLARE_ACCOUNT_ID` |

Cloudflare 另一種做法是後台 **Workers & Pages → Connect to Git** 直接連這個 repo，
不需要 token 也不需要 workflow——那樣的話請把 `cloudflare.yml` 刪掉，
否則一次 push 會部署兩次。

本機預覽：

```bash
npx serve public
```

## 授權

程式碼可自由使用。數據為各資料來源所有。
