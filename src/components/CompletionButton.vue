<template>
  <button 
    class="completion-button"
    :disabled="!enabled"
    @click="$emit('complete')"
  >
    合併完成
  </button>
</template>

<script setup>
defineProps({
  enabled: {
    type: Boolean,
    default: false
  }
});

defineEmits(['complete']);
</script>

<style scoped>
.completion-button {
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 0.75rem 2rem;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.completion-button:hover:not(:disabled) {
  background-color: #35a372;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
  transform: translateY(-1px);
}

.completion-button:active:not(:disabled) {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.completion-button:disabled {
  background-color: #cccccc;
  color: #666666;
  cursor: not-allowed;
  opacity: 0.6;
}
</style>
