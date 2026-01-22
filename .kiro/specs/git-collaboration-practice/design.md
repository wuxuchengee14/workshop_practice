# 設計文檔

## 概述

Git 多人協作練習專案是一個基於 Vue.js 3 的單頁式應用（SPA），專為教學 Git 分支管理和衝突解決而設計。此應用提供一個簡單但有效的環境，讓多位學員可以同時修改相同的內容區域，從而在合併時產生真實的衝突場景。

### 設計目標

1. **簡單性**：最小化的 UI 和功能，專注於 Git 操作練習
2. **衝突可預測性**：確保學員修改會產生可控的合併衝突
3. **教學友善**：清晰的視覺回饋和狀態指示
4. **易於設置**：標準的 Vue.js 專案結構，易於安裝和運行

## 架構

### 技術棧

- **前端框架**：Vue.js 3.x（使用 Composition API）
- **構建工具**：Vite
- **樣式**：CSS（可選使用 Scoped CSS）
- **版本控制**：Git
- **套件管理**：npm

### 專案結構

```
git-collaboration-practice/
├── .git/                    # Git 儲存庫
├── public/                  # 靜態資源
├── src/
│   ├── components/
│   │   ├── ContentArea.vue  # 內容區塊組件
│   │   └── CompletionButton.vue  # 完成按鈕組件
│   ├── App.vue              # 根組件
│   ├── main.js              # 應用入口
│   └── style.css            # 全域樣式
├── .gitignore
├── index.html
├── package.json
├── vite.config.js
└── README.md                # 練習說明
```

### 應用架構

應用採用簡單的單頁架構，不需要路由或狀態管理庫：

```
App.vue (根組件)
├── ContentArea.vue (內容區塊)
└── CompletionButton.vue (完成按鈕)
```

## 組件與介面

### 1. App.vue（根組件）

**職責**：
- 作為應用的主容器
- 管理完成狀態（isCompleted）
- 協調子組件之間的互動

**Props**：無

**State**：
- `isCompleted: boolean` - 追蹤練習是否完成
- `isButtonEnabled: boolean` - 控制完成按鈕是否可點擊

**Methods**：
- `handleCompletion()` - 處理完成按鈕點擊事件

**Template 結構**：
```vue
<template>
  <div id="app">
    <header>
      <h1>Git 多人協作練習</h1>
    </header>
    
    <main>
      <ContentArea />
    </main>
    
    <footer>
      <CompletionButton 
        :enabled="isButtonEnabled"
        @complete="handleCompletion"
      />
      <div v-if="isCompleted" class="completion-message">
        合併完成！課程結束
      </div>
    </footer>
  </div>
</template>
```

### 2. ContentArea.vue（內容區塊組件）

**職責**：
- 顯示可被學員修改的內容區域
- 這是產生合併衝突的主要區域

**Props**：無

**State**：
- `content: string` - 顯示的文字內容

**Template 結構**：
```vue
<template>
  <div class="content-area">
    <h2>請修改以下內容</h2>
    <div class="editable-content">
      {{ content }}
    </div>
    <p class="instruction">
      請在您的分支上修改上方的文字內容
    </p>
  </div>
</template>
```

### 3. CompletionButton.vue（完成按鈕組件）

**職責**：
- 顯示完成按鈕
- 根據 enabled prop 控制按鈕狀態
- 發出完成事件

**Props**：
- `enabled: boolean` - 控制按鈕是否可點擊

**Events**：
- `complete` - 當按鈕被點擊時發出

**Template 結構**：
```vue
<template>
  <button 
    class="completion-button"
    :disabled="!enabled"
    @click="$emit('complete')"
  >
    合併完成
  </button>
</template>
```

## 資料模型

### 應用狀態

由於應用非常簡單，不需要複雜的狀態管理。所有狀態都在組件內部管理：

```typescript
interface AppState {
  isCompleted: boolean;      // 練習是否完成
  isButtonEnabled: boolean;  // 按鈕是否啟用（初始為 false）
}

interface ContentAreaState {
  content: string;  // 預設內容文字
}
```

### 初始資料

**ContentArea 預設內容**：
```
這是一個 Git 協作練習專案。
請在您的分支上修改這段文字。
```

**App 初始狀態**：
```javascript
{
  isCompleted: false,
  isButtonEnabled: false  // 講師需要手動改為 true
}
```

## 正確性屬性

*屬性是一個特徵或行為，應該在系統的所有有效執行中保持為真——本質上是關於系統應該做什麼的正式陳述。屬性作為人類可讀規範和機器可驗證正確性保證之間的橋樑。*


### 屬性反思

在分析驗收標準後，我發現大部分需求涉及 Git 的標準功能（分支管理、衝突處理等），這些不是我們應用本身的功能。可測試的屬性主要集中在：

1. UI 組件的渲染和狀態
2. 按鈕的啟用/禁用邏輯
3. 完成訊息的顯示

由於這是一個簡單的教學應用，可測試的屬性數量有限，主要是 UI 行為的驗證。

### 正確性屬性

**屬性 1：按鈕狀態反映 enabled prop**

*對於任何* enabled 布林值，當 CompletionButton 組件接收到該 prop 時，按鈕的 disabled 屬性應該等於 !enabled

**驗證需求：需求 6.2**

**屬性 2：點擊啟用按鈕觸發完成事件**

*對於任何* 啟用狀態（enabled=true）的 CompletionButton，當按鈕被點擊時，應該發出 'complete' 事件

**驗證需求：需求 6.3**

**屬性 3：完成狀態顯示訊息**

*對於任何* App 組件狀態，當 isCompleted 為 true 時，應該在 DOM 中渲染包含文字「合併完成！課程結束」的元素

**驗證需求：需求 6.3**

## 錯誤處理

### 使用者操作錯誤

1. **禁用按鈕點擊**：
   - 當按鈕處於禁用狀態時，點擊不應觸發任何事件
   - Vue.js 的 `:disabled` 綁定會自動處理此情況

2. **重複點擊**：
   - 完成訊息顯示後，重複點擊按鈕不應產生副作用
   - 通過檢查 `isCompleted` 狀態來防止重複處理

### 開發環境錯誤

1. **依賴安裝失敗**：
   - README.md 應包含故障排除指南
   - 確保 package.json 中的依賴版本相容

2. **開發伺服器啟動失敗**：
   - 檢查端口是否被佔用
   - 提供替代端口配置說明

## 測試策略

### 單元測試

使用 Vitest 和 Vue Test Utils 進行組件測試：

1. **ContentArea.vue 測試**：
   - 驗證組件正確渲染
   - 驗證預設內容文字存在
   - 驗證說明文字存在

2. **CompletionButton.vue 測試**：
   - 驗證按鈕文字為「合併完成」
   - 驗證 enabled=false 時按鈕被禁用
   - 驗證 enabled=true 時按鈕可點擊
   - 驗證點擊時發出 'complete' 事件

3. **App.vue 測試**：
   - 驗證初始狀態（isCompleted=false, isButtonEnabled=false）
   - 驗證子組件正確渲染
   - 驗證 handleCompletion 方法設置 isCompleted=true
   - 驗證完成訊息在 isCompleted=true 時顯示

### 屬性測試

使用 fast-check 進行屬性測試（最少 100 次迭代）：

1. **屬性 1 測試**：
   - 標籤：**Feature: git-collaboration-practice, Property 1: 按鈕狀態反映 enabled prop**
   - 生成隨機布林值作為 enabled prop
   - 驗證按鈕的 disabled 屬性正確反映

2. **屬性 2 測試**：
   - 標籤：**Feature: git-collaboration-practice, Property 2: 點擊啟用按鈕觸發完成事件**
   - 測試啟用狀態的按鈕點擊
   - 驗證事件被正確發出

3. **屬性 3 測試**：
   - 標籤：**Feature: git-collaboration-practice, Property 3: 完成狀態顯示訊息**
   - 生成隨機的 isCompleted 狀態
   - 驗證訊息顯示與狀態一致

### 整合測試

1. **端到端流程**：
   - 啟動應用
   - 驗證初始狀態（按鈕禁用）
   - 手動修改程式碼啟用按鈕
   - 點擊按鈕
   - 驗證完成訊息顯示

### Git 操作測試（手動）

由於 Git 操作是此專案的核心教學目標，需要手動測試：

1. **分支創建測試**：
   - 從 main 分支創建新分支
   - 驗證分支成功創建

2. **內容修改測試**：
   - 在分支上修改 ContentArea.vue 中的內容
   - 提交變更
   - 驗證變更被記錄

3. **衝突產生測試**：
   - 多個分支修改相同內容
   - 嘗試合併
   - 驗證衝突被正確標記

4. **衝突解決測試**：
   - 手動解決衝突
   - 完成合併
   - 驗證合併成功

## 樣式設計

### 佈局

- 使用 Flexbox 進行垂直佈局
- 內容區塊置中顯示
- 完成按鈕固定在底部

### 視覺設計原則

1. **簡潔性**：最小化的視覺元素，避免分散注意力
2. **清晰性**：明確的視覺層次和狀態指示
3. **可讀性**：適當的字體大小和行距

### 色彩方案

- 主色：#42b983（Vue.js 綠色）
- 背景：#f5f5f5（淺灰色）
- 文字：#2c3e50（深灰色）
- 禁用狀態：#cccccc（灰色）

### 響應式設計

- 支援桌面和平板尺寸
- 最小寬度：320px
- 內容區塊最大寬度：800px

## 部署考量

### 開發環境

- Node.js 版本：18.x 或更高
- npm 版本：9.x 或更高
- 開發伺服器：Vite dev server（預設端口 5173）

### 生產構建

雖然此專案主要用於教學，但仍可構建生產版本：

```bash
npm run build
```

生產檔案將輸出到 `dist/` 目錄。

### Git 儲存庫設置

1. **初始提交**：包含完整的專案結構和預設內容
2. **分支保護**：建議保護 main 分支，要求 pull request
3. **.gitignore**：排除 node_modules、dist 等目錄

## 擴展性考量

### 未來可能的增強功能

1. **多個衝突區域**：增加更多可修改的內容區塊
2. **學員名單**：顯示參與練習的學員列表
3. **進度追蹤**：追蹤每位學員的合併狀態
4. **自動化檢查**：檢測分支和合併狀態

### 保持簡單

由於此專案的主要目的是教學 Git 操作，應避免過度複雜化應用本身。任何新功能都應該服務於 Git 學習目標。
