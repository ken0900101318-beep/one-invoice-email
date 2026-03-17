# ONE桌遊 發票 Email 收集系統

## 📋 功能說明

### 前台（業者填寫）
- 業者搜尋自己的店名
- 確認店家資訊
- 填寫接收電子發票的 Email
- 手機可用

### 後台（管理查看）
- 查看所有店家
- 統計填寫進度
- 篩選已填寫/未填寫
- 匯出 Email 清單（CSV）

---

## 🚀 部署步驟

### 步驟 1：建立 Google 試算表

1. 前往 [Google Sheets](https://sheets.google.com)
2. 建立新試算表，命名為：`ONE桌遊發票Email資料`
3. 複製試算表網址中的 ID（格式：`https://docs.google.com/spreadsheets/d/【這段是ID】/edit`）
4. 記下這個 ID

---

### 步驟 2：設定 Google Apps Script

1. 在試算表中，點擊 **擴充功能 → Apps Script**
2. 刪除預設的 Code.gs 內容
3. 將 `Code.gs.txt` 的內容貼上
4. **修改第 5 行**：將 `你的試算表ID` 替換成剛剛複製的 ID
5. 點擊 **執行 → initializeSheet** （初始化試算表）
6. 授權（第一次需要授權存取試算表）
7. 點擊 **部署 → 新增部署**
8. 類型選：**網頁應用程式**
9. 設定：
   - 執行身分：**我**
   - 具有存取權限的使用者：**所有人**
10. 點擊 **部署**
11. 複製**網頁應用程式網址**（重要！）

---

### 步驟 3：匯入店家資料

1. 回到 Apps Script 編輯器
2. 開啟 `stores.json`，複製所有內容
3. 在 Code.gs 找到 `importJsonData` 函式
4. 將 JSON 內容貼到 `const jsonData = []` 的 `[]` 裡面
5. 執行 **執行 → importJsonData**
6. 回到試算表，確認資料已匯入

---

### 步驟 4：設定前台網址

1. 開啟 `index.html`
2. 找到第 178 行：`const GAS_URL = 'https://...'`
3. 替換成剛剛複製的**網頁應用程式網址**
4. 儲存

---

### 步驟 5：設定後台網址

1. 開啟 `admin.html`
2. 找到第 207 行：`const GAS_URL = 'https://...'`
3. 替換成剛剛複製的**網頁應用程式網址**
4. 儲存

---

### 步驟 6：上傳到 GitHub Pages

1. 建立新的 GitHub 倉庫：`one-invoice-email`
2. 上傳 `index.html` 和 `admin.html`
3. 啟用 GitHub Pages（Settings → Pages → Source: main branch）
4. 取得網址：`https://你的帳號.github.io/one-invoice-email/`

---

## 📱 使用網址

### 前台（給業者）
```
https://你的帳號.github.io/one-invoice-email/
```

### 後台（你自己）
```
https://你的帳號.github.io/one-invoice-email/admin.html
```

---

## 🔗 整合到管理系統

在 `one-management-portal` 的 `menu.html` 中，新增一個系統連結：

```javascript
{
    name: "發票Email收集",
    url: "https://你的帳號.github.io/one-invoice-email/admin.html",
    icon: "📧",
    color: "from-pink-400 to-rose-500",
    status: "active"
}
```

---

## 📂 檔案說明

- `Code.gs.txt` - Google Apps Script 後端程式碼
- `index.html` - 前台（業者填寫頁面）
- `admin.html` - 後台（管理查看頁面）
- `stores.json` - 店家資料（用於匯入到試算表）
- `README.md` - 此說明文件

---

## ⚠️ 注意事項

1. **試算表權限**：確保試算表的「具有連結的任何人」設定為「檢視者」或以上
2. **GAS 網址**：每次重新部署 Apps Script 都會產生新的網址，記得更新 HTML
3. **資料備份**：定期備份試算表資料
4. **測試**：部署後先自己測試填寫一次

---

## 🆘 疑難排解

### 問題：點擊「送出 Email」沒反應
- 檢查瀏覽器 Console 是否有錯誤
- 確認 `GAS_URL` 是否正確
- 確認 Apps Script 已部署且權限設定為「所有人」

### 問題：後台看不到資料
- 確認試算表有資料
- 確認 `GAS_URL` 是否正確
- 重新整理頁面

### 問題：無法匯入 JSON 資料
- 確認 JSON 格式正確（可用 jsonlint.com 檢查）
- 確認已授權 Apps Script 存取試算表

---

## 📞 技術支援

如有問題，請聯絡系統管理員。
