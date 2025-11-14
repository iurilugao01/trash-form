<script setup lang="ts">
import { computed } from "vue";

const props = withDefaults(
  defineProps<{
    customStyle?: string[];
  }>(),
  {
    customStyle: () => ["bg-indigo-600", "text-white"],
  }
);

const baseButtonClass = [
  "px-4",
  "py-2",
  "rounded",
  "font-semibold",
  "transition-all",
  "duration-200",
  "ease-in-out",
  "focus:outline-none",
  "shadow",
  "hover:shadow-lg",
  "active:scale-95",
  "hover:brightness-110",
  "disabled:opacity-70",
  "disabled:cursor-not-allowed",
];

const buttonClasses = computed(() => {
  return [...baseButtonClass, ...(props.customStyle ?? [])];
});
</script>

<template>
  <button :class="buttonClasses">
    <slot />
  </button>
</template>

<style scoped>
button {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}
button:active {
  transform: scale(0.96);
}
</style>
