<template>
  <div class="icon-list-container">
    <div class="icon-list row q-col-gutter-y-md">
      <icon-list-item class="col-12" v-for="(image) of images" :key="image.src" :image="image"/>
    </div>
  </div>
</template>

<style scoped lang="scss">
.icon-list {
  max-width: 1200px;
}
</style>

<script setup lang="ts">
import IconListItem from './IconListItem.vue';
import { ImageInfo } from 'favicons-scraper';

export type IconListProps = {
  images: ImageInfo[];
}

const props = defineProps<IconListProps>()
</script>