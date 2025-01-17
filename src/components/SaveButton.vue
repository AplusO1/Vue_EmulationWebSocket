<template>
  <button :disabled="!messages.length" @click="saveMessages">
    Сохранить переписку
  </button>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

interface Message {
  text: string;
  timestamp: string;
}

export default defineComponent({
  name: 'SaveButton',
  props: {
    messages: {
      type: Array as PropType<Message[]>,
      required: true,
    },
  },
  methods: {
    saveMessages() {
      const content = this.messages
        .map((msg) => `[${msg.timestamp}] ${msg.text}`)
        .join('\n');
      const blob = new Blob([content], { type: 'text/plain' });
      const link = document.createElement('a');
      const timestamp = new Date().toISOString().replace(/[:.]/g, '-');
      link.href = URL.createObjectURL(blob);
      link.download = `chat_${timestamp}.txt`;
      link.click();
      alert('Переписка успешно сохранена!');
    },
  },
});
</script>

<style scoped>
button {
  padding: 12px 24px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  font-weight: bold;
  transition: background-color 0.3s ease;
}
button:disabled {
  background-color: #e0e0e0;
  cursor: not-allowed;
}
button:hover:not(:disabled) {
  background-color: #43a047;
}
</style>