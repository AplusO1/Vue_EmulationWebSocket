<template>
  <div class="chat">
    <h1 class="title">Чат</h1>
    <div class="messages">
      <p v-if="!messages.length" class="no-messages">Новых сообщений нет!</p>
      <Message 
        v-for="(message, index) in messages" 
        :key="index" 
        :text="message.text" 
        :timestamp="message.timestamp"
      />
    </div>
    <div class="input-container">
      <input v-model="newMessage" @keyup.enter="addMessage" placeholder="Введите сообщение..." />
      <button @click="addMessage">Добавить сообщение</button>
    </div>
    <SaveButton :messages="messages" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue';
import Message from './Message.vue';
import SaveButton from './SaveButton.vue';

interface Message {
  text: string;
  timestamp: string;
}

export default defineComponent({
  name: 'Chat',
  components: { Message, SaveButton },
  setup() {
    const messages = reactive<Message[]>([]);
    const newMessage = ref('');

    const addMessage = () => {
      if (!newMessage.value.trim()) return;
      const now = new Date();
      messages.push({
        text: newMessage.value.trim(),
        timestamp: now.toLocaleTimeString(),
      });
      newMessage.value = '';
    };

    return {
      messages,
      newMessage,
      addMessage,
    };
  },
});
</script>

<style scoped>
.title {
  text-align: center;
}
.chat {
  padding: 20px;
  max-width: 600px;
  margin: 0 auto;
  font-family: 'Helvetica Neue', sans-serif;
  color: #333;
}
.messages {
  border: 1px solid #e0e0e0;
  padding: 10px;
  margin-bottom: 20px;
  max-height: 300px;
  overflow-y: auto;
  background-color: #f9f9f9;
  border-radius: 8px;
}
.input-container {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 14px;
}
button {
  padding: 12px 24px;
  background-color: #ff5a5f;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  font-weight: bold;
  transition: background-color 0.3s ease;
}
button:hover {
  background-color: #e04848;
}
</style>