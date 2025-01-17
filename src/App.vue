<template>
  <div id="app">
    <Chat />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Chat from './components/Chat.vue';

export default defineComponent({
  name: 'App',
  components: {
    Chat,
  },
});
</script>

<style>
body {
  margin: 0;
  font-family: 'Helvetica Neue', Arial, sans-serif;
  background-color: #f4f4f9;
  color: #333;
}
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}
</style>