<script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import {type Message, CkcAnswer } from 'ckc-ui'
  import { message } from './const/mock-data/message8';
  import { setCustomComponents } from 'markstream-vue';
  import 'markstream-vue/index.css';
  import HelloWorld from './components/HelloWorld.vue';
  import 'ckc-ui/dist/style.css';
  
  setCustomComponents('docs', {
    'custom-data': HelloWorld,
  })
  const messages = ref<Message[]>([]);

  onMounted(() => {
    let index = 0;
    const addMessage = () => {
      if (index < message.length) {
        messages.value.push(message[index] as Message);
        index++;
        setTimeout(addMessage, 50); // 每秒添加一条消息，模拟流式返回
      }
    };
    addMessage();
  });
</script>

<template>
  <CkcAnswer :messages="messages" render-custom-id="docs" :custom-html-tags="['custom-data']">
    <template #actions="actionsProps">
        <button @click="messages = []">清空消息</button>
        {{ actionsProps.messageViewInfo }}
    </template>
  </CkcAnswer>
</template>
<style>

</style>
