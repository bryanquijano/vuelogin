<template>
  <h1 class="text-6xl font-thin tracking-tighter text-center mt-8 text-white">
    Cool Chat
  </h1>
  <div
    class="min-h-[500px] w-full mt-8 rounded-lg shadow-2xl flex flex-col justify-between bg-gray-700 text-white"
  >
    <ul class="p-4 space-y-4">
      <li v-for="n in 5">
        <div class="flex justify-between bg-gray-600 px-4 py-2 rounded-lg">
          <span>Message itself </span>
          <span>by Author Name</span>
        </div>
      </li>
    </ul>
    <div class="border-t-2 border-gray-500">
      <input
        class="w-full p-4 focus:outline-none focus:bg-gray-600 bg-gray-700"
        type="text"
        placeholder="Type a message..."
      />
    </div>
  </div>
</template>
