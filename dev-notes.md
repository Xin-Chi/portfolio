# 開發筆記

## 即時預覽伺服器

### 使用技術：browser-sync

**browser-sync** 是一個 Node.js 套件，功能是：
1. 在本地端建立一個 HTTP 伺服器，讓你用瀏覽器開啟 HTML 檔案
2. 監聽指定檔案的變動（watching files）
3. 當你存檔後，自動透過 WebSocket 通知瀏覽器重新整理（live reload）

### 啟動指令

```bash
cd "C:/Users/lex/Desktop/sideproject"
nohup npx browser-sync start --server --files "*.html, **/*.css, **/*.js" --port 3000 --no-notify > /tmp/bs.log 2>&1 &
```

| 參數 | 說明 |
|------|------|
| `--server` | 在目前資料夾啟動靜態 HTTP 伺服器 |
| `--files` | 監聽這些檔案的變動，存檔後自動重載 |
| `--port 3000` | 指定 port（若被佔用會自動遞增，例如 3002） |
| `--no-notify` | 不在瀏覽器右上角顯示 "Connected to BrowserSync" 提示 |
| `nohup ... &` | 讓程序在背景持續運行，關閉終端後不會中斷 |

### 開啟網站

啟動後在瀏覽器輸入：

```
http://localhost:3000/webvc.html
```

（若 3000 被佔用，port 會自動改為 3002、3004 等，請看啟動 log）

### 停止伺服器

```bash
kill $(lsof -t -i:3000)
# 或查詢 PID 後手動 kill
ps aux | grep browser-sync
```

### 環境需求

- **Node.js** v16+（已安裝：v16.15.0）
- **npx**：Node.js 內建，無需另外安裝 browser-sync，npx 會自動下載
- **Python 3.12.7**（已安裝，備用，可用 `python -m http.server` 做簡單伺服器，但無 live reload 功能）

---

## 網站檔案結構

```
sideproject/
├── webvc.html          # 主頁（個人資料、自傳、技能、專案連結）
├── thesis.html         # 碩論頁面
├── capstone.html       # 專題頁面
├── side-project.html   # Side Project（待填內容）
├── webphoto.jpg        # 個人照片
├── thesis/             # 碩論相關圖片
└── capstone/           # 專題相關圖片與 PDF
```
