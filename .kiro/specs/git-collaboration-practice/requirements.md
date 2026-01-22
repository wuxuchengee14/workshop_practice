# 需求文檔

## 簡介

Git 多人協作練習專案是一個基於 Vue.js 的單頁式網頁應用，旨在為學員提供實際的 Git 分支管理和衝突解決練習環境。學員將通過修改共享的網頁內容來體驗真實的合併衝突場景，並學習如何正確解決這些衝突。

## 術語表

- **System（系統）**：Git 多人協作練習專案的 Vue.js 網頁應用
- **Learner（學員）**：使用此專案進行 Git 練習的學習者
- **Instructor（講師）**：指導學員並示範衝突解決的教學者
- **Content_Div（內容區塊）**：網頁中間用於學員修改的指定 div 容器
- **Completion_Button（完成按鈕）**：網頁底部顯示「合併完成」的按鈕
- **Main_Branch（主分支）**：Git 儲存庫的 main 分支
- **Learner_Branch（學員分支）**：每位學員創建的個人工作分支

## 需求

### 需求 1：專案初始化與設置

**使用者故事：** 作為學員，我想要從 GitHub 拉取專案到本地，以便開始 Git 協作練習。

#### 驗收標準

1. THE System SHALL 提供一個可通過 Git clone 下載的 GitHub 儲存庫
2. WHEN 學員執行 git clone 命令 THEN THE System SHALL 包含一個完整可運行的 Vue.js 專案
3. THE System SHALL 包含必要的專案配置檔案（package.json、vite.config.js 等）
4. THE System SHALL 包含 README.md 檔案，說明專案設置和練習步驟

### 需求 2：分支管理

**使用者故事：** 作為學員，我想要創建自己的分支並在其上工作，以便練習 Git 分支操作。

#### 驗收標準

1. WHEN 學員創建新分支 THEN THE System SHALL 允許分支從 Main_Branch 分出
2. THE System SHALL 支援多個 Learner_Branch 同時存在
3. WHEN 學員在 Learner_Branch 上進行修改 THEN THE System SHALL 不影響其他分支的內容

### 需求 3：網頁內容結構

**使用者故事：** 作為學員，我想要看到一個包含可修改內容區塊和完成按鈕的網頁，以便進行練習。

#### 驗收標準

1. THE System SHALL 在網頁中間顯示一個 Content_Div
2. THE Content_Div SHALL 包含可被學員修改的文字內容
3. THE System SHALL 在網頁底部顯示一個 Completion_Button
4. THE Completion_Button SHALL 顯示文字「合併完成」
5. WHEN 專案初始化完成 THEN THE Completion_Button SHALL 處於禁用狀態（disabled）

### 需求 4：內容修改與衝突產生

**使用者故事：** 作為學員，我想要修改內容區塊的文字，以便在合併時產生衝突並學習解決方法。

#### 驗收標準

1. WHEN 學員在 Learner_Branch 上修改 Content_Div 的內容 THEN THE System SHALL 保存這些變更
2. WHEN 多位學員修改相同的 Content_Div 內容 THEN THE System SHALL 在合併時產生衝突
3. THE System SHALL 允許學員提交（commit）他們的修改到 Learner_Branch

### 需求 5：合併衝突處理

**使用者故事：** 作為講師，我想要示範如何解決合併衝突，以便教導學員正確的衝突解決流程。

#### 驗收標準

1. WHEN 學員嘗試將 Learner_Branch 合併回 Main_Branch THEN THE System SHALL 檢測到衝突（如果存在）
2. WHEN 衝突發生 THEN THE System SHALL 在衝突檔案中標記衝突區域
3. THE System SHALL 允許講師手動解決衝突並完成合併
4. WHEN 所有衝突解決完成 THEN THE System SHALL 允許合併提交到 Main_Branch

### 需求 6：完成狀態管理

**使用者故事：** 作為講師，我想要在所有合併完成後啟用完成按鈕，以便標示練習結束。

#### 驗收標準

1. THE System SHALL 允許講師手動修改 Completion_Button 的狀態
2. WHEN 講師將 Completion_Button 改為啟用狀態 THEN THE Completion_Button SHALL 變為可點擊
3. WHEN 學員點擊已啟用的 Completion_Button THEN THE System SHALL 顯示訊息「合併完成！課程結束」
4. THE System SHALL 在顯示完成訊息時保持網頁的其他內容可見

### 需求 7：Vue.js 應用架構

**使用者故事：** 作為開發者，我想要使用 Vue.js 框架構建此應用，以便提供現代化的前端開發體驗。

#### 驗收標準

1. THE System SHALL 使用 Vue.js 3.x 作為前端框架
2. THE System SHALL 使用單檔案組件（Single File Components）架構
3. THE System SHALL 包含必要的 Vue.js 依賴套件
4. WHEN 執行 npm install THEN THE System SHALL 安裝所有必要的依賴
5. WHEN 執行 npm run dev THEN THE System SHALL 啟動開發伺服器並顯示網頁
