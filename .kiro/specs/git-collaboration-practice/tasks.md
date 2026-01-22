# 實作計畫：Git 多人協作練習專案

## 概述

此實作計畫將 Git 多人協作練習專案分解為一系列可執行的編碼任務。專案使用 Vue.js 3 和 Vite 構建，重點在於創建一個簡單但有效的環境來練習 Git 分支管理和衝突解決。

## 任務

- [x] 1. 設置專案結構和配置
  - 初始化 Vite + Vue 3 專案
  - 配置 package.json 包含必要的依賴（vue, vite）
  - 創建 .gitignore 檔案（排除 node_modules, dist, .DS_Store 等）
  - 創建基本的專案目錄結構（src/components, public）
  - _需求：1.2, 1.3, 7.1, 7.3_

- [ ] 2. 實作 ContentArea 組件
  - [x] 2.1 創建 ContentArea.vue 單檔案組件
    - 使用 Composition API 定義組件
    - 定義 content 響應式資料（預設文字：「這是一個 Git 協作練習專案。請在您的分支上修改這段文字。」）
    - 實作 template 包含標題、內容區塊和說明文字
    - 添加 scoped CSS 樣式
    - _需求：3.1, 3.2, 7.2_

  - [ ]* 2.2 撰寫 ContentArea 組件的單元測試
    - 測試組件正確渲染
    - 測試預設內容文字存在
    - 測試說明文字存在
    - _需求：3.1, 3.2_

- [ ] 3. 實作 CompletionButton 組件
  - [x] 3.1 創建 CompletionButton.vue 單檔案組件
    - 定義 enabled prop（type: Boolean, default: false）
    - 實作按鈕 template，綁定 disabled 屬性到 !enabled
    - 按鈕文字設為「合併完成」
    - 添加 click 事件處理，發出 'complete' 事件
    - 添加 scoped CSS 樣式（包含禁用狀態樣式）
    - _需求：3.3, 3.4, 3.5, 6.2_

  - [ ]* 3.2 撰寫 CompletionButton 組件的單元測試
    - 測試按鈕文字為「合併完成」
    - 測試 enabled=false 時按鈕被禁用
    - 測試 enabled=true 時按鈕可點擊
    - 測試點擊時發出 'complete' 事件
    - _需求：3.3, 3.4, 3.5, 6.2_

  - [ ]* 3.3 撰寫屬性測試：按鈕狀態反映 enabled prop
    - **屬性 1：按鈕狀態反映 enabled prop**
    - **驗證需求：6.2**
    - 使用 fast-check 生成隨機布林值
    - 驗證按鈕的 disabled 屬性等於 !enabled
    - 配置最少 100 次迭代
    - 標籤：**Feature: git-collaboration-practice, Property 1: 按鈕狀態反映 enabled prop**

  - [ ]* 3.4 撰寫屬性測試：點擊啟用按鈕觸發完成事件
    - **屬性 2：點擊啟用按鈕觸發完成事件**
    - **驗證需求：6.3**
    - 測試 enabled=true 的按鈕點擊
    - 驗證 'complete' 事件被發出
    - 配置最少 100 次迭代
    - 標籤：**Feature: git-collaboration-practice, Property 2: 點擊啟用按鈕觸發完成事件**

- [ ] 4. 實作 App 根組件
  - [x] 4.1 創建 App.vue 根組件
    - 使用 Composition API 定義組件
    - 定義響應式狀態：isCompleted（初始值 false）、isButtonEnabled（初始值 false）
    - 實作 handleCompletion 方法（設置 isCompleted = true）
    - 實作 template 包含 header、main（ContentArea）、footer（CompletionButton 和完成訊息）
    - 綁定 CompletionButton 的 enabled prop 到 isButtonEnabled
    - 綁定 CompletionButton 的 @complete 事件到 handleCompletion
    - 使用 v-if 條件渲染完成訊息（當 isCompleted 為 true）
    - _需求：3.1, 3.3, 6.3, 6.4_

  - [ ]* 4.2 撰寫 App 組件的單元測試
    - 測試初始狀態（isCompleted=false, isButtonEnabled=false）
    - 測試子組件正確渲染
    - 測試 handleCompletion 方法設置 isCompleted=true
    - 測試完成訊息在 isCompleted=true 時顯示
    - 測試完成訊息包含文字「合併完成！課程結束」
    - _需求：3.5, 6.3, 6.4_

  - [ ]* 4.3 撰寫屬性測試：完成狀態顯示訊息
    - **屬性 3：完成狀態顯示訊息**
    - **驗證需求：6.3**
    - 使用 fast-check 生成隨機的 isCompleted 布林值
    - 驗證當 isCompleted=true 時，DOM 包含「合併完成！課程結束」文字
    - 驗證當 isCompleted=false 時，DOM 不包含該文字
    - 配置最少 100 次迭代
    - 標籤：**Feature: git-collaboration-practice, Property 3: 完成狀態顯示訊息**

- [x] 5. 檢查點 - 確保所有測試通過
  - 確保所有測試通過，如有問題請詢問使用者

- [ ] 6. 實作全域樣式和佈局
  - [x] 6.1 創建 src/style.css 全域樣式檔案
    - 定義 CSS 變數（色彩方案：主色 #42b983、背景 #f5f5f5、文字 #2c3e50）
    - 設置全域字體和基本樣式
    - 實作 Flexbox 佈局樣式（垂直佈局、內容置中）
    - 設置響應式斷點（最小寬度 320px、內容最大寬度 800px）
    - _需求：3.1, 3.3, 6.4_

  - [x] 6.2 在 App.vue 中應用佈局樣式
    - 為 #app 容器添加 Flexbox 樣式
    - 為 header、main、footer 添加適當的間距和對齊
    - 確保完成訊息顯示時不遮擋其他內容
    - _需求：6.4_

- [ ] 7. 設置應用入口和配置
  - [x] 7.1 創建 src/main.js 入口檔案
    - 導入 Vue 的 createApp
    - 導入 App 組件和全域樣式
    - 創建並掛載 Vue 應用到 #app
    - _需求：7.1_

  - [x] 7.2 創建 index.html 根 HTML 檔案
    - 設置基本 HTML 結構
    - 包含 #app 掛載點
    - 引入 main.js 作為模組
    - _需求：1.2_

  - [x] 7.3 配置 vite.config.js
    - 導入 Vue 插件
    - 配置基本的 Vite 設定
    - _需求：1.3_

- [ ] 8. 創建專案文檔
  - [x] 8.1 撰寫 README.md
    - 專案簡介和目的
    - 安裝步驟（git clone、npm install）
    - 運行步驟（npm run dev）
    - Git 練習流程說明：
      1. 創建個人分支
      2. 修改 ContentArea.vue 中的內容文字
      3. 提交變更
      4. 嘗試合併回 main 分支
      5. 解決衝突
      6. 講師啟用完成按鈕（修改 App.vue 中的 isButtonEnabled）
      7. 點擊按鈕查看完成訊息
    - 故障排除指南
    - _需求：1.4_

- [x] 9. 檢查點 - 最終驗證
  - 確保所有測試通過
  - 驗證應用可以正常啟動（npm run dev）
  - 驗證所有組件正確渲染
  - 驗證按鈕初始狀態為禁用
  - 手動測試：修改 isButtonEnabled 為 true，驗證按鈕可點擊
  - 手動測試：點擊按鈕，驗證完成訊息顯示
  - 如有問題請詢問使用者

- [ ] 10. Git 儲存庫初始化和提交
  - [ ] 10.1 初始化 Git 儲存庫
    - 執行 git init
    - 創建初始提交（包含所有專案檔案）
    - _需求：1.1_

  - [ ] 10.2 準備衝突測試環境
    - 確保 ContentArea.vue 中的內容文字容易被修改
    - 確保 App.vue 中的 isButtonEnabled 容易被講師修改
    - 在 README.md 中標註這些關鍵修改點
    - _需求：4.1, 6.1_

## 注意事項

- 標記 `*` 的任務為可選任務，可以跳過以加快 MVP 開發
- 每個任務都引用了具體的需求編號以確保可追溯性
- 檢查點確保增量驗證
- 屬性測試驗證通用正確性屬性
- 單元測試驗證具體範例和邊界情況
- 測試框架：Vitest + Vue Test Utils + fast-check
