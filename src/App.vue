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

<script setup>
import { ref } from 'vue';
import ContentArea from './components/ContentArea.vue';
import CompletionButton from './components/CompletionButton.vue';

// 定義響應式狀態
const isCompleted = ref(false);
const isButtonEnabled = ref(false);

// 實作 handleCompletion 方法
const handleCompletion = () => {
  isCompleted.value = true;
};
</script>

<style scoped>
/* #app 容器的 Flexbox 樣式已在 style.css 中定義 */
/* 這裡為各個區塊添加適當的間距和對齊 */

header {
  text-align: center;
  padding: 2rem 1rem;
  flex-shrink: 0; /* 防止 header 被壓縮 */
}

main {
  flex: 1; /* 佔據剩餘空間 */
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem 1rem;
  min-height: 0; /* 允許內容正確縮放 */
}

footer {
  text-align: center;
  padding: 2rem 1rem;
  flex-shrink: 0; /* 防止 footer 被壓縮 */
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

/* 完成訊息樣式 - 確保不遮擋其他內容 */
.completion-message {
  color: #42b983;
  font-size: 1.2rem;
  font-weight: 600;
  padding: 1rem 2rem;
  background-color: #f0f9f4;
  border-radius: 4px;
  border: 2px solid #42b983;
  margin-top: 0.5rem;
  max-width: 100%;
  box-sizing: border-box;
}
</style>
