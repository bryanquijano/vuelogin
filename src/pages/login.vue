<script setup>
import { onBeforeMount, ref } from "vue";
import { useRouter } from "vue-router";
import useAuth from "../composable/useAuth";
import useError from "../composable/useError";

const { isAuthenticated, login, signup } = useAuth();

const username = ref("");
const password = ref("");

const router = useRouter();

const logginIn = async () => {
  await login(username.value, password.value);
  goToHome();
};

const signingUp = async () => {
  await signup(username.value, password.value);
  goToHome();
};

const goToHome = () => {
  // If user is authenticated, send them to the home page
  if (isAuthenticated.value) {
    router.push("/");
  } else {
    setError("Invalid username or password");
    start();
  }
};

const { error, setError } = useError();

import { useTimeout, promiseTimeout } from "@vueuse/core";

const { ready, start } = useTimeout(3000, { controls: true });
</script>

<template>
  <div
    class="flex flex-col justify-center items-center min-h-screen-nonav bg-inherit"
  >
    <!-- Logged in: {{ isAuthenticated }} -->
    <div
      class="flex shadow-2xl rounded-lg justify-center items-center bg-gray-300 overflow-hidden"
    >
      <img class="h-64" src="../assets/bglogin.png" alt="Hello GB" />
      <form @submit.prevent="logginIn" class="flex flex-col space-y-4 p-4">
        <input
          type="text"
          class="border-2 p-2 rounded-lg border-gray-500"
          placeholder="Username"
          v-model="username"
        />
        <input
          type="password"
          class="border-2 p-2 rounded-lg border-gray-500"
          placeholder="Password"
          v-model="password"
        />
        <div class="flex space-x-2">
          <button
            type="submit"
            @submit.prevent="logginIn"
            class="bg-green-600 text-green-100 py-4 rounded-lg w-1/2 hover:bg-green-800 hover:text-white"
          >
            Login
          </button>
          <button
            @click="signingUp"
            class="border-2 border-gray-500 text-blue-800 py-4 rounded-lg w-1/2 hover:bg-gray-400 hover:text-white hover:border-gray-900"
          >
            Sign Up
          </button>
        </div>
      </form>
    </div>
    <div
      v-if="!ready && error"
      class="bg-red-300 w-1/4 absolute bottom-2 right-2 rounded-lg p-4 text-center text-red-800"
    >
      {{ error }}
    </div>
  </div>
</template>
