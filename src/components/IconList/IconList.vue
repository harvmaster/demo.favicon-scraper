<template>
  <div class="list-item-container">
    <div class="list-item row">
      <icon-list-item class="col-12" v-for="(image, index) of images" :key="image.src" :image="image" :visible-size="visibleSizes[index]"/>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>

<script setup lang="ts">
import { ref, computed  } from 'vue'
import IconListItem from './IconListItem.vue';
import { ImageInfo } from 'favicons-scraper';

export type IconListProps = {
  images: ImageInfo[];
}

const props = defineProps<IconListProps>()

const visibleSizes = computed(() => {
  const min = 32 as const;
  const max = 128 as const;

  const scale = (max - min) / (props.images.length - 1);

  return props.images.map((_, i) => {
    const width = min + i * scale;
    const height = width;

    return { width, height };
  });
})
</script>