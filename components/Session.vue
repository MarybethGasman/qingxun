<template>
  <a :href="`/rooms/${msg.id}`" class="bg-white flex justify-between">
    <div>
      <img :src="msg.imgUrl" alt="">
    </div>
    <div class="flex-1">
      <h2>{{ msg.name }}</h2>
      <p class="font-thin text-sm">{{ msg.lastMessage }}</p>
    </div>
    <div class="font-thin text-sm">
      {{ msg.date }}
    </div>
  </a>

</template>

<script lang="ts" setup>
interface Message {
  id: number;
  name: string;
  imgUrl: string;
  lastMessage: string;
  date: string;
}
const msg = defineProps<Message>();
</script>
  
<style lang="css" scoped>
</style>