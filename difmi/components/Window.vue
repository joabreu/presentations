<script setup lang="ts">
/**
 * An Apple style window with a dark bar up top with three colored dots.
 */

const props = defineProps<{
  /**
   * The windows title.
   */
  title: string;
}>();
</script>

<template>
  <div
    class="
      apple-window
      baum-window
      console
      text-xs
      relative
      object-cover
      z-10
      flex-grow
      pt-6
    "
  >
    <div
      class="absolute top-0 flex flex-row w-full px-3 py-2"
      style="height: 1.5rem; background-color: var(--slidev-code-foreground); max-height: 100%; border-radius: 8px 8px 0px 0px;"
    >
      <ul class="grid grid-cols-4 gap-3">
        <li class="!m-0 rounded w-2 h-2 bg-red-400 inline-block"></li>
        <li class="!m-0 rounded w-2 h-2 bg-yellow-300 inline-block"></li>
        <li class="!m-0 rounded w-2 h-2 bg-green-500 inline-block"></li>
      </ul>
      <div
        class="
          absolute
          top-1
          flex flex-row
          w-full
          justify-center
          items-center
        "
      >
        <span class="inline-block" style="color: var(--slidev-code-background)">{{ props.title }}</span>
      </div>
    </div>
    <slot />
  </div>
</template>

<style scoped>
.apple-window {
  box-shadow: var(--slidev-code-background);
  border: var(--slidev-code-background);
  border-radius: 0.375rem 0.375rem 0 0;
}
</style>
