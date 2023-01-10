<template>
  <div>
    <!-- {{ $route.params.id }} -->
    <div class="overflow-y-hidden h-[100vh] w-80 m-auto relative">
      <header class="sticky flex flex-row-reverse">
        <div>添加</div>
        <div>搜索</div>
        <h2 class="absolute w-full text-center">微信</h2>
      </header>

      <main class="h-[100vh] overflow-y-scroll">
        <section class="max-h-full">chat room {{ $route.params.id }}</section>
        <Message v-for="m in msgList" :content="m"/>
      </main>
      <footer class="bg-white sticky bottom-1 w-full flex">
        <textarea v-model="msg" class="h-8 resize-none flex-1" name="" id=""></textarea>
        <button class="block bg-green-400" @click="sendMsg">发送</button>
      </footer>
    </div>
  </div>
</template>

<script setup lang="ts">
let ws: WebSocket, msg
let msgList = ref([])
let sendMsg = () => {
  ws.send(msg)
  msg = ""
}
onMounted(() => {
  if (process.client) {
    ws = new WebSocket("ws://192.168.43.62:8081");
    ws.onopen = () => {
      ws.send("hello");
    };
    ws.onmessage = (e) => {
      msgList.value = [...msgList.value, e.data]
      // console.log(msgList.value)
    }
  }
});
</script>

<style lang="css" scoped>
</style>