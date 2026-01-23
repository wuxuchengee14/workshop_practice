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

### 1. 複製 Git 練習專案

```bash
git clone <repository-url>
cd git-collaboration-practice
```

### 2. 安裝依賴項

```bash
npm install
```

> **注意**：請確保您已安裝 Node.js 18.x 或更高版本。

## 運行步驟

### 啟動開發伺服器

```bash
npm run dev
```

開發伺服器將在啟動專案後的終端列中輸出端口。

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

## 專案結構

```
git-collaboration-practice/
├── src/
│   ├── components/
│   │   ├── ContentArea.vue      # 內容區塊組件
│   │   └── CompletionButton.vue # 完成按鈕組件
│   ├── App.vue                   # 根組件
│   ├── main.js                   # 應用入口
│   └── style.css                 # 全域樣式
├── public/                       # 靜態資源
├── index.html                    # HTML 入口
├── package.json                  # 專案配置
├── vite.config.js               # Vite 配置
└── README.md                     # 本檔案
```

## 故障排除指南

### 問題：開發伺服器無法啟動

**可能原因**：端口 5173 被佔用

**解決方法**：
```bash
# 使用其他端口啟動
npm run dev -- --port 3000
```

### 問題：Git 命令執行失敗

**可能原因**：未配置 Git 使用者資訊

**解決方法**：
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```