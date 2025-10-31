<script setup lang="ts">
import { ref } from "vue";
import BaseButton from "./BaseButton.vue";

const firstName = ref<string[]>([]);
const index = ref(0);
const deny = ref(false);

const nextLetter = () => {
  if (deny.value) return;
  if (firstName.value[index.value] != undefined) index.value++;
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
  <div class="flex flex-col gap-4">
    <div class="flex gap-4">
      <label>Insira seu nome</label>
      <i class="bi bi-hand-index" @click="insertLetter"></i>
      <i class="bi bi-hand-thumbs-up" @click="nextLetter"></i>

      <BaseButton @click="confirm" />
    </div>
    <div>
      <input
        :value="firstName.join('')"
        class="bg-blac p-2k"
        type="text"
        disabled
      />
    </div>
    <div v-if="deny">
      <span class="text-red-700">
        <i class="bi bi-info-circle"></i>
        Nomes começam com letra maiuscula imbecil
      </span>
    </div>
  </div>
</template>
