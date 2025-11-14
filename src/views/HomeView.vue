<script setup lang="ts">
import TheFirstQuestion from "../components/TheFirstQuestion.vue";
import TheSecondQuestion from "../components/TheSecondQuestion.vue";
</script>

<template>
  <div class="">
    <form>
      <h1 class="text-4xl font-bold mb-6">O pior formulario da historia</h1>

      <div
        class="flex flex-col gap-4 min-h-[320px] items-center justify-center bg-slate-950 py-12"
      >
        <TheFirstQuestion />
        <TheSecondQuestion />
      </div>
    </form>
  </div>
</template>
