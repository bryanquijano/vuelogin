<script setup>
import { onUnmounted, ref } from "vue";
import useChat from "../composable/useChat";
import useAuth from "../composable/useAuth";

const { messages, unsubscribe, sendMessage } = useChat();
const { user } = useAuth();

const newMessage = ref("");

const send = () => {
  sendMessage(newMessage.value);
  newMessage.value = "";
};

onUnmounted(() => {
  unsubscribe();
});
</script>

<template>
  <h1 class="text-6xl font-thin tracking-tighter text-center mt-8 text-white">
    Bryan's Real-Time Chat App
  </h1>
  <div
    class="min-h-[500px] w-full my-8 rounded-lg shadow-2xl flex flex-col justify-between bg-gray-700 text-white"
  >
    <ul class="p-4 space-y-4">
      <li v-for="message in messages" :key="message.id">
        <div
          class="flex justify-between px-4 py-4 rounded-lg hover:bg-gray-900"
          :class="user === message.author ? 'bg-gray-500' : 'bg-gray-800'"
        >
          <span>{{ message.text }} </span>
          <span>by {{ message.author }}</span>
        </div>
        <p class="text-xs text-gray-400">{{ message.createdAt }}</p>
      </li>
    </ul>
    <div class="border-t-2 border-gray-500">
      <input
        class="w-full p-4 focus:outline-none focus:bg-gray-600 bg-gray-700"
        type="text"
        placeholder="Type a message..."
        v-model="newMessage"
        @change="send"
      />
    </div>
  </div>
</template>
