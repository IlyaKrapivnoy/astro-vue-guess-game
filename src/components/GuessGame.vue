<template>
  <div class="min-h-screen flex items-center justify-center">
    <div class="flex flex-col items-center space-y-4 p-4 max-w-md">
      <h2 class="text-2xl font-semibold text-2xl">Угадай число от 1 до 100</h2>
      <input
        v-model.number="guess"
        type="number"
        placeholder="Ваш вариант"
        class="border px-2 py-1 rounded w-full"
      />
      <button
        @click="checkGuess"
        class="bg-blue-500 text-white px-4 py-2 rounded"
      >
         Проверить
      </button>
      <p v-if="message" class="text-lg">{{ message }}</p>
      <button @click="resetGame" class="text-sm text-gray-500 underline mt-2">
        Начать заново
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const guess = ref(null);
const target = ref(Math.floor(Math.random() * 100) + 1);
const message = ref("");

const checkGuess = () => {
  if (guess.value === target.value) {
    message.value = "Угадал!";
  } else if (guess.value < target.value) {
    message.value = "Больше";
  } else {
    message.value = "Меньше";
  }
};

const resetGame = () => {
  guess.value = null;
  target.value = Math.floor(Math.random() * 100) + 1;
  message.value = "";
};
</script>
