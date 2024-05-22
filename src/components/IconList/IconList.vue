<template>
  <div class="icon-list-container">
    <div class="icon-list row">
      <icon-list-item class="col-12" v-for="(image) of images" :key="image.src" :image="image"/>
    </div>
  </div>
</template>

<style scoped lang="scss">
.icon-list {
  max-width: 1200px;

  .icon-list-item {
    margin: 0.5rem;
  }

  .icon-list-item {
    display: flex;
    align-items: center;
    padding: 0.5rem;
    background-color: white;
    border-radius: 0.5rem;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
  }
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