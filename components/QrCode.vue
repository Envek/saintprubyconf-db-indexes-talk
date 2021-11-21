<script setup lang="ts">
const props = defineProps({
  url: {
    type: String,
  },
  caption: {
    type: String,
  },
  class: {
    type: String,
  },
})
</script>

<template>
  <figure class="qr-code-container py-2 px-4" :class="props.class">
    <a :href="props.url">
      <qr-code-vue :value="props.url" class="scaled-image w-full h-full" render-as="svg" />
      <figcaption class="text-center py-1">{{props.caption}}</figcaption>
    </a>
  </figure>
</template>

<style scoped>
  .qr-code-container figcaption {
    font-size: 0.5rem;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    font-stretch: 3%;
  }
</style>
