<template>
  <div ref="IconListContainer" :style="listContainerStyle">
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
import { computed, nextTick, ref, watch } from 'vue';
import IconListItem from './IconListItem.vue';
import { ImageInfo } from 'favicons-scraper';

export type IconListProps = {
  images: ImageInfo[];
}

const props = defineProps<IconListProps>()
const emits = defineEmits<{
  resize: [number]
}>()

const IconListContainer = ref<HTMLElement | null>(null)
const listContainerStyle = ref({ height: `0px` })
const getListContainerStyle = () => {
  const children = IconListContainer.value?.children
  if (!children) return { height: `0px` }
  console.log(children)

  const height = Array.from(children).reduce((acc, child) => {
    return acc + child.clientHeight
  }, 0)

  console.log('height 2', height)

  emits('resize', height)

  return { height: `${height}px` }
}

watch(() => props.images, () => {
  nextTick(() => {
    listContainerStyle.value = getListContainerStyle()
  })
})
</script>