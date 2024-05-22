<template>
  <div class="list-item-container">
    <div class="list-item row">
      <div class="col-auto">
        <q-img :src="image.src" :alt="image.src" :aspect-ratio="1" :width="visibleSize.width.toString()"/>
      </div>

      <div class="col">
        {{ image.src }}
      </div>

    </div>
  </div>
</template>

<style scoped lang="scss">

</style>

<script setup lang="ts">
import { defineProps } from 'vue'
import { ImageInfo } from 'favicons-scraper'

export type IconListItemProps = {
  image: ImageInfo;
  visibleSize: {
    width: number;
    height: number;
  }
}

const props = defineProps<IconListItemProps>()
</script>