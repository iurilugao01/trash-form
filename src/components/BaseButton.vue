<script setup lang="ts">
const props = defineProps<{
  customStyle?: string[];
}>();
</script>

<template>
  <button :class="props.customStyle"></button>
</template>
