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
      text-xs
      relative
      pt-5
    "
  >
    <div
      class="absolute top-0 bg-gray-300 flex flex-row w-full px-3 py-2"
      style="height: 1.5rem; max-height: 100%; border-radius: 8px 8px 0px 0px;"
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
        <span class="inline-block text-black">{{ props.title }}</span>
      </div>
    </div>
    <div class="no-border">
      <slot />
    </div>
  </div>
</template>

<style>
.no-border > .slidev-code-wrapper > pre {
  border-radius: 0 0 8px 8px !important;
}
</style>
