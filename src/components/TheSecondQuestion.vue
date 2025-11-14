<script setup lang="ts">
import { ref } from "vue";
import BaseButton from "./BaseButton.vue";

const lastName = ref<string[]>([]);
const index = ref(0);
const deny = ref(false);

const nextLetter = () => {
  if (deny.value) return;
  if (lastName.value[index.value] != undefined) index.value++;
};
const insertLetter = () => {
  if (deny.value) return;
  const letter = firstName.value[index.value];
  switch (letter) {
    case "z":
      firstName.value[index.value] = "A";
      break;
    case "Z":
      break;
    case undefined:
      firstName.value[index.value] = "a";
      break;
    default:
      if (letter.toUpperCase() === letter) {
        firstName.value[index.value] = String.fromCharCode(
          letter.toUpperCase().charCodeAt(0) + 1
        );
        break;
      }
      firstName.value[index.value] = String.fromCharCode(
        letter.charCodeAt(0) + 1
      );
      break;
  }

  console.log(firstName.value);
};

const confirm = () => {
  if (deny.value) return;

  if (firstName.value[0]?.toUpperCase() !== firstName.value[0]) {
    deny.value = true;
    return;
  }
  alert(`Seu nome é ${firstName.value.join("")}`);
};
</script>

<template>
  <div
    class="flex flex-col items-center bg-gray-900 shadow-lg rounded-lg px-8 py-8 gap-8 w-full max-w-md"
  >
    <div class="flex flex-col w-full gap-3">
      <label
        class="text-lg font-semibold text-gray-200 flex items-center gap-2 mb-1"
      >
        <i class="bi bi-person-circle text-2xl text-gray-300"></i>
        Insira seu sobrenome
      </label>
      <div class="flex flex-row items-center gap-3 justify-between w-full">
        <div class="flex flex-row gap-2">
          <button
            @click="insertLetter"
            class="flex items-center justify-center w-10 h-10 rounded-full hover:scale-110 bg-gray-700 hover:bg-gray-600 text-gray-100 transition"
            title="Inserir próxima letra"
          >
            <i class="bi bi-hand-index text-indigo-300 text-xl"></i>
          </button>
          <button
            @click="nextLetter"
            class="flex items-center justify-center w-10 h-10 rounded-full hover:scale-110 bg-gray-700 hover:bg-gray-600 text-gray-100 transition"
            title="Próxima posição"
          >
            <i class="bi bi-hand-thumbs-up text-indigo-300 text-xl"></i>
          </button>
        </div>
        <BaseButton
          @click="confirm"
          :customStyle="[
            'bg-emerald-700',
            'hover:bg-emerald-800',
            'text-gray-100',
            'px-5',
            'py-2',
            'border',
            'border-emerald-900',
          ]"
        >
          <span class="flex items-center gap-2">
            <i class="bi bi-check-circle text-lg text-emerald-200"></i>
            Confirmar
          </span>
        </BaseButton>
      </div>
    </div>
    <div class="w-full">
      <input
        :value="firstName.join('')"
        class="w-full border-2 border-gray-700 rounded-md bg-gray-800 text-gray-100 px-4 py-2 text-lg font-mono focus:outline-gray-400 transition"
        type="text"
        readonly
      />
    </div>
    <transition name="fade">
      <div v-if="deny" class="w-full flex items-center justify-center mt-2">
        <span
          class="inline-flex items-center rounded bg-red-900 px-3 py-2 text-red-100 font-medium text-base shadow border border-red-700 gap-2 animate-shake"
        >
          <i class="bi bi-info-circle-fill text-xl text-red-200"></i>
          Nomes começam com letra maiúscula!
        </span>
      </div>
    </transition>
  </div>
</template>

<style scoped>
@keyframes shake {
  0% {
    transform: translateX(0);
  }
  20% {
    transform: translateX(-6px);
  }
  40% {
    transform: translateX(6px);
  }
  60% {
    transform: translateX(-4px);
  }
  80% {
    transform: translateX(4px);
  }
  100% {
    transform: translateX(0);
  }
}
.animate-shake {
  animation: shake 0.35s;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
