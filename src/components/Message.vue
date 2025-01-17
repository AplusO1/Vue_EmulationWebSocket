<template>
  <div class="message">
    <p>{{ text }}</p>
    <span class="timestamp">{{ timestamp }}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Message',
  props: {
    text: {
      type: String,
      required: true,
    },
    timestamp: {
      type: String,
      required: true,
    },
  },
});
</script>

<style scoped>
.message {
  padding: 10px;
  border-bottom: 1px solid #e0e0e0;
  background-color: #ffffff;
  border-radius: 4px;
  margin-bottom: 8px;
  transition: transform 0.2s;
}
.message:hover {
  transform: scale(1.02);
}
.timestamp {
  display: block;
  font-size: 0.8em;
  color: #999;
  margin-top: 5px;
}
</style>