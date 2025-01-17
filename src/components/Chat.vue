<template>
  <div class="chat">
    <h1 class="title">Чат</h1>
    <div class="messages">
      <Message 
        v-for="(message, index) in messages" 
        :key="index" 
        :text="message.text" 
        :timestamp="message.timestamp"
      />
    </div>
    <button @click="addMessage">Добавить сообщение</button>
    <SaveButton :messages="messages" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';
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

    const addMessage = () => {
      const now = new Date();
      messages.push({
        text: `Сообщение ${messages.length + 1}`,
        timestamp: now.toLocaleTimeString(),
      });
    };

    return {
      messages,
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
