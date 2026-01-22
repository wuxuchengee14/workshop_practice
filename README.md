# Git 多人協作練習專案

這是一個基於 Vue.js 3 的單頁式應用，專為教學 Git 分支管理和衝突解決而設計。學員將通過修改共享的網頁內容來體驗真實的合併衝突場景，並學習如何正確解決這些衝突。

## 專案目的

本專案提供一個簡單但有效的環境，讓多位學員可以：
- 練習 Git 分支的創建和管理
- 體驗真實的合併衝突場景
- 學習如何解決合併衝突
- 理解多人協作開發的工作流程

## 技術棧

- **前端框架**：Vue.js 3.x（Composition API）
- **構建工具**：Vite
- **測試框架**：Vitest + Vue Test Utils + fast-check
- **版本控制**：Git

## 安裝步驟

### 1. 克隆專案

```bash
git clone <repository-url>
cd git-collaboration-practice
```

### 2. 安裝依賴

```bash
npm install
```

> **注意**：請確保您已安裝 Node.js 18.x 或更高版本。

## 運行步驟

### 啟動開發伺服器

```bash
npm run dev
```

開發伺服器將在 `http://localhost:5173` 啟動（預設端口）。

### 其他可用命令

```bash
# 構建生產版本
npm run build

# 預覽生產構建
npm run preview

# 運行測試
npm test

# 運行測試（UI 模式）
npm run test:ui
```

## Git 練習流程說明

### 步驟 1：創建個人分支

從 `main` 分支創建您的個人工作分支：

```bash
git checkout -b your-name-branch
```

例如：`git checkout -b alice-branch`

### 步驟 2：修改內容文字

打開 `src/components/ContentArea.vue` 檔案，找到以下部分：

```vue
<script setup>
import { ref } from 'vue'

const content = ref('這是一個 Git 協作練習專案。請在您的分支上修改這段文字。')
</script>
```

**修改 `content` 變數的文字內容**，例如：

```javascript
const content = ref('這是 Alice 的修改：學習 Git 協作真有趣！')
```

### 步驟 3：提交變更

將您的修改提交到您的分支：

```bash
git add src/components/ContentArea.vue
git commit -m "修改內容文字"
```

### 步驟 4：嘗試合併回 main 分支

切換回 `main` 分支並嘗試合併您的分支：

```bash
git checkout main
git merge your-name-branch
```

**如果其他學員已經修改並合併了相同的內容**，您將會看到合併衝突！

### 步驟 5：解決衝突

當發生衝突時，Git 會在 `ContentArea.vue` 中標記衝突區域：

```javascript
<<<<<<< HEAD
const content = ref('這是 Bob 的修改：Git 衝突解決很重要！')
=======
const content = ref('這是 Alice 的修改：學習 Git 協作真有趣！')
>>>>>>> your-name-branch
```

**手動編輯檔案**，決定要保留哪些內容或合併兩者：

```javascript
const content = ref('這是 Alice 和 Bob 的共同修改：學習 Git 協作和衝突解決都很重要！')
```

刪除衝突標記（`<<<<<<<`、`=======`、`>>>>>>>`），然後：

```bash
git add src/components/ContentArea.vue
git commit -m "解決合併衝突"
```

### 步驟 6：講師啟用完成按鈕

當所有學員都完成合併後，**講師**將修改 `src/App.vue` 檔案：

找到以下部分：

```vue
<script setup>
import { ref } from 'vue'
import ContentArea from './components/ContentArea.vue'
import CompletionButton from './components/CompletionButton.vue'

const isCompleted = ref(false)
const isButtonEnabled = ref(false)  // 講師將此改為 true

const handleCompletion = () => {
  isCompleted.value = true
}
</script>
```

**將 `isButtonEnabled` 的初始值從 `false` 改為 `true`**：

```javascript
const isButtonEnabled = ref(true)  // 啟用按鈕
```

提交變更：

```bash
git add src/App.vue
git commit -m "啟用完成按鈕"
```

### 步驟 7：點擊按鈕查看完成訊息

重新整理網頁（或重新啟動開發伺服器），您將看到「合併完成」按鈕已啟用。

點擊按鈕後，將顯示訊息：**「合併完成！課程結束」**

🎉 恭喜！您已完成 Git 多人協作練習！

## 專案結構

```
git-collaboration-practice/
├── src/
│   ├── components/
│   │   ├── ContentArea.vue      # 內容區塊組件（學員修改此檔案）
│   │   └── CompletionButton.vue # 完成按鈕組件
│   ├── App.vue                   # 根組件（講師修改此檔案啟用按鈕）
│   ├── main.js                   # 應用入口
│   └── style.css                 # 全域樣式
├── public/                       # 靜態資源
├── index.html                    # HTML 入口
├── package.json                  # 專案配置
├── vite.config.js               # Vite 配置
└── README.md                     # 本檔案
```

## 故障排除指南

### 問題 1：npm install 失敗

**可能原因**：Node.js 版本過舊

**解決方法**：
```bash
# 檢查 Node.js 版本
node --version

# 如果版本低於 18.x，請升級 Node.js
# 訪問 https://nodejs.org/ 下載最新版本
```

### 問題 2：開發伺服器無法啟動

**可能原因**：端口 5173 被佔用

**解決方法**：
```bash
# 使用其他端口啟動
npm run dev -- --port 3000
```

### 問題 3：合併衝突標記無法識別

**可能原因**：編輯器未正確顯示衝突標記

**解決方法**：
- 使用支援 Git 的編輯器（如 VS Code）
- 或使用 `git status` 查看衝突檔案
- 手動搜尋 `<<<<<<<` 標記

### 問題 4：修改後網頁未更新

**可能原因**：瀏覽器快取

**解決方法**：
- 硬性重新整理：`Ctrl + Shift + R`（Windows/Linux）或 `Cmd + Shift + R`（Mac）
- 或清除瀏覽器快取

### 問題 5：Git 命令執行失敗

**可能原因**：未配置 Git 使用者資訊

**解決方法**：
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## 學習資源

- [Git 官方文檔](https://git-scm.com/doc)
- [Vue.js 官方文檔](https://vuejs.org/)
- [Vite 官方文檔](https://vitejs.dev/)

## 授權

本專案僅供教學使用。

---

**祝您學習愉快！如有任何問題，請向講師尋求協助。**