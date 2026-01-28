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

<script setup>
import { ref } from 'vue';

const content = ref('這是一個 Git 協作練習專案。');
</script>

<style scoped>
.content-area {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.content-area h2 {
  color: #2c3e50;
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  text-align: center;
}

.editable-content {
  background-color: #f5f5f5;
  border: 2px solid #42b983;
  border-radius: 4px;
  padding: 1.5rem;
  font-size: 1.1rem;
  line-height: 1.6;
  color: #2c3e50;
  min-height: 100px;
  margin-bottom: 1rem;
}

.instruction {
  color: #666;
  font-size: 0.9rem;
  text-align: center;
  font-style: italic;
  margin-top: 1rem;
}
</style>
