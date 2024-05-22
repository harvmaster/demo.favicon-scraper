<template>
  <div>
    <div class="icon-list row q-col-gutter-y-md">
      <transition-group name="icon-list-expand" mode="out-in" tag="div" class="col-12 row q-col-gutter-y-md">
        <icon-list-item class="col-12" v-for="(image) of images" :key="image.src" :image="image"/>
      </transition-group>
    </div>
  </div>
</template>

<style scoped lang="scss">
.icon-list {
  max-width: 1200px;
  overflow-x: scroll;
  overflow-y: hidden;
}

// .icon-list-expand-move,
// .icon-list-expand-enter-active, .icon-list-expand-leave-active {
//   transition: all 0.5s;
// }
// .icon-list-expand-enter-from, .icon-list-expand-leave-to {
//   opacity: 0;
//   max-height: 0px;
// }
// .icon-list-expand-leave-active {
//   position: absolute;
// }
</style>

<script setup lang="ts">
import IconListItem from './IconListItem.vue';
import { ImageInfo } from 'favicons-scraper';

export type IconListProps = {
  images: ImageInfo[];
}

const props = defineProps<IconListProps>()s
</script>