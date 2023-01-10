<template>
  <div class="font-thin text-sm">
    {{ msg.content }}
  </div>
</template>
  
  <script lang="ts" setup>
interface Message {
  content: string;
}
const msg = defineProps<Message>();
</script>
    
  <style lang="css" scoped>
</style>