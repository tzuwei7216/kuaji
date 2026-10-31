# 快記 — 快速記賬 PWA

打開就能記一筆，資料存在手機本機，可離線使用，並可匯出 CSV / Excel 到電腦分析。

## 功能

- 大鍵盤快速記一筆，支出 / 收入切換
- 分類可自訂（新增、刪除）
- 每月明細（依日期分組）與結餘
- 分類統計長條圖
- 匯出 CSV、匯出 Excel（含「明細」+「分類統計」兩個工作表）
- 刪單筆 / 刪整月 / 全部清空
- 深淺色自動切換，也可手動切換
- 加到主畫面後可離線使用（透過 service worker）

## 檔案說明（全部放在 repo 根目錄）

| 檔案 | 用途 |
|---|---|
| `index.html` | App 本體（HTML + CSS + JS） |
| `manifest.json` | PWA 設定（名稱、圖示、顏色、全螢幕） |
| `sw.js` | Service worker，快取 app 讓它離線可用 |
| `icon.svg` | App 圖示 |

> 這 4 個檔案用相對路徑互相連結，**必須放在同一層（repo 最外層）**，不要放進子資料夾。

## 部署到 GitHub Pages

1. 新建一個 repo（例如 `kuaiji`），設為 **Public**。
2. 把上面 4 個檔案上傳到 repo 根目錄
   （網頁：Add file → Upload files；或用 git push）。
3. 進 repo 的 **Settings → Pages**：
   - Source：`Deploy from a branch`
   - Branch：`main`，資料夾：`/ (root)`，按 Save。
4. 等一兩分鐘，Pages 會給一個網址，像
   `https://你的帳號.github.io/kuaiji/`。
5. 手機瀏覽器打開那個網址 → 加到主畫面：
   - iPhone（Safari）：分享 → 加入主畫面
   - Android（Chrome）：⋮ → 加到主畫面 / 安裝應用程式

完成後桌面會多一個圖示，點開就是全螢幕的記賬 app。

### 用 git 上傳（選用）

```bash
git init
git add index.html manifest.json sw.js icon.svg README.md
git commit -m "快記 PWA"
git branch -M main
git remote add origin https://github.com/你的帳號/kuaiji.git
git push -u origin main
```

## 資料與備份

- 記賬資料存在**手機瀏覽器的本機儲存**（localStorage），不會上傳到任何伺服器。
- 換手機、清除瀏覽器網站資料、或改用不同網址開啟，資料都不會跟著走，請先用「下載 CSV / Excel」備份。
- 更新 app（重新上傳 `index.html`）不會清掉已記的資料，因為網址（來源）沒變。

## 自訂

- **分類**：在 app 內「記帳」頁，分類區塊的「＋ 管理」可增刪。
- **顏色 / 名稱 / 預設分類**：改 `index.html` 最上面 `:root` 的色票，或 JS 裡的 `DEFAULT_CATS`；app 名稱改 `manifest.json` 的 `name` / `short_name` 與 `index.html` 的 `<title>`。

## 離線說明

匯出 Excel 需要載入一個元件（SheetJS CDN），第一次使用請連網；CSV 匯出與記賬本身完全離線可用。
