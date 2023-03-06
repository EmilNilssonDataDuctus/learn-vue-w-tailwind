<template>
  <div
    v-show="modalActive"
    class="absolute top-0 left-0 flex justify-center w-full h-screen px-8 bg-black bg-opacity-30"
  >
    <div
      v-if="modalActive"
      class="self-start max-w-screen-md p-4 mt-32 bg-white"
    >
      <slot />
      <button
        class="px-6 py-2 mt-8 text-white bg-weather-primary"
        @click="$emit('close-modal')"
      >
        Close
      </button>
    </div>
  </div>
</template>

<script setup>
defineEmits(["close-modal"]);
defineProps({
  modalActive: {
    type: Boolean,
    default: false,
  },
});
</script>

<style lang="scss" scoped></style>
