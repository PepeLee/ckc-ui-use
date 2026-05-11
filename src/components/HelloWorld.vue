<script setup lang="ts">
import { ref, watch } from 'vue';
import JSON5 from 'json5';

const props = defineProps<{
  node: {
    type: string
    content?: string
    loading?: boolean
  }
  customId?: string
  isDark?: boolean
}>()
const customData = ref<Record<string, any> | null>(null)
watch(
    () => props.node.content as string,
    (content) => {
        if (!content) return;
        try {
            if (!content.startsWith('{') || !content.endsWith('}')) {
                return
            }
            console.log(props,content)
            const validJsonStr = content.replace(/‘|’/g, '"')
            customData.value = JSON5.parse(validJsonStr)
            console.log('Parsed custom-data:', customData.value)
        } catch (error) {
            console.error('Failed to parse custom-data:', error)
        }
    },
    { immediate: true }
)
</script>

<template>
  <div>
     {{ props.node.loading }}
      -{{ customData?.day }}
  </div>
</template>
