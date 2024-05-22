<template>
  <div class="icon-list-item-container">
    <div class="icon-list-item row">
      <div class="col-auto">
        <q-img :src="image.src" :alt="image.src" :aspect-ratio="1" :width="`${Math.min(Math.floor(image.size.width), 64).toString()}px`"/>
      </div>

      <div class="col">
        {{ image.src }}
      </div>

    </div>
  </div>
</template>

<style scoped lang="scss">
.icon-list-item {
  display: flex;
  align-items: center;
  padding: 0.5rem;
  background-color: white;
  border-radius: 0.5rem;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
}
</style>

<script setup lang="ts">
import { defineProps } from 'vue'
import { ImageInfo } from 'favicons-scraper'

export type IconListItemProps = {
  image: ImageInfo;
}

const props = defineProps<IconListItemProps>()
</script>