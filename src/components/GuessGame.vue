<template>
  <div class="min-h-screen flex items-center justify-center">
    <div class="flex flex-col items-center space-y-4 p-4 max-w-md">
      <h2 class="font-semibold text-2xl text-[#5f5f5f]">
        Угадай число от 1 до 100
      </h2>
      <input
        v-model.number="guess"
        type="number"
        placeholder="Твой вариант"
        class="custom-input"
        min="0"
        max="100"
        @input="clampGuess"
      />
      <button @click="checkGuess" class="custom-button">Проверить</button>
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

const clampGuess = (event) => {
  const value = event.target.valueAsNumber;
  if (value < 0 || isNaN(value)) {
    guess.value = 0;
  } else if (value > 100) {
    guess.value = 100;
  } else {
    guess.value = value;
  }
};

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

<style scoped>
.custom-input {
  @apply w-[190px] w-full border-none outline-none bg-transparent text-lg text-gray-600 pt-[15px] pr-[5px] pb-[10px] pl-[20px] rounded-[25px];
  box-shadow: inset 8px 8px 8px #cbced1, inset -8px -8px 8px #ffffff;
}

.custom-input::placeholder {
  @apply text-gray-600 transition-all duration-300 ease-in-out;
}

.custom-input:focus::placeholder {
  @apply text-gray-400;
}

.custom-button {
  @apply text-gray-900 px-6 py-3 text-lg rounded-lg bg-gray-200 border border-gray-200 cursor-pointer transition-all duration-300;
  box-shadow: 6px 6px 12px #c5c5c5, -6px -6px 12px #ffffff;
}

.custom-button:active {
  @apply text-gray-600;
  box-shadow: inset 4px 4px 12px #c5c5c5, inset -4px -4px 12px #ffffff;
}
</style>
