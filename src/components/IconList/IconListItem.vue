<template>
  <div class="icon-list-item-container">
    <div class="icon-list-item row" :style="`height: ${iconStyle.height}`">
      <div class="col-auto q-pr-md">
        <q-img :src="image.src" :alt="image.src" :aspect-ratio="1" :width="iconStyle.width"/>
      </div>

      <div class="col row self-center">
        <span class="col-12 image-src">
          {{ image.src }}
        </span>
        <span class="col-12">
          {{ image.size.width }}x{{ image.size.height }}
        </span>
      </div>

    </div>
  </div>
</template>

<style scoped lang="scss">
// .icon-list-item {
//   display: flex;
//   align-items: center;
//   padding: 0.5rem;
//   background-color: white;
//   border-radius: 0.5rem;
//   box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
// }
.image-src {
  font-size: 1.5rem;
}
.icon-list-item {
  transform: translateX(0);
  transition: transform 0.2s;
}
.icon-list-item:hover {
  background-color: #834694;
  border-radius: 1000em;
  transform: translateX(1.05%);

}
</style>

<script setup lang="ts">
import { computed, defineProps } from 'vue'
import { ImageInfo } from 'favicons-scraper'

export type IconListItemProps = {
  image: ImageInfo;
}

const props = defineProps<IconListItemProps>()

const iconStyle = computed(() => {
  return {
    height: `${Math.min(Math.floor(props.image.size.height), 64)}px`,
    width: `${Math.min(Math.floor(props.image.size.width), 64)}px`
  }
})
</script>