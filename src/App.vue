<script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import {type Message, CkcAnswer } from 'ckc-ui'
  import { message1 } from './const/mock-data/message1';
  import { setCustomComponents } from 'markstream-vue';
  import 'markstream-vue/index.css';
  import HelloWorld from './components/HelloWorld.vue';
  
  setCustomComponents('docs', {
    'custom-data': HelloWorld,
  })
  const messages = ref<Message[]>([]);

  onMounted(() => {
    let index = 0;
    const addMessage = () => {
      if (index < message1.length) {
        messages.value.push(message1[index] as Message);
        index++;
        setTimeout(addMessage, 120); // 每秒添加一条消息，模拟流式返回
      }
    };
    addMessage();
  });
</script>

<template>
  <CkcAnswer :messages="messages" render-custom-id="docs" :custom-html-tags="['custom-data']"></CkcAnswer>
</template>
