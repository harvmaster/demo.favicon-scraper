<template>
  <div class="icon-list-item-container">
    <div class="icon-list-item row" :style="`min-height: ${iconStyle.height}`" @click="expand">
      <div class="col-auto self-center q-pr-md">
        <q-img :src="image.src" :alt="image.src" :aspect-ratio="1" :width="iconStyle.width"/>
      </div>

      <div class="col row self-center">
        <span class="col-12 image-src">
          {{ image.src }}
        </span>
      </div>

    </div>
    <div ref="expandedContent" class="expanded-content" :style="expandedStyle">
      <div class="row q-pt-md">
        <div class="col-12">
          <q-separator style="background-color: #8e8e8e" />
        </div>
        <div class="col-12 row justify-between">
          <div class="col row">
            <div class="col-auto row q-pa-md fit-width">
              <span class="col-12">Width: {{ image.size.width }}</span>
              <span class="col-12">Height: {{ image.size.height }}</span>
            </div>
            <div class="col-auto row q-pa-md">
              <span class="col-12">Type: {{ image.type }}</span>
            </div>
          </div>
          <div class="col-auto row q-pa-md">
            <button class="col-auto open-button" color="#834694" icon="open_in_new" @click="openImage">
              Go to image →
            </button>
          </div>
        </div>
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
.fit-width {
  width: fit-content;
}
.image-src {
  font-size: 1.5rem;
  overflow: scroll;
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
.expanded-content {
  overflow: hidden;
  transition: height 0.2s;
}
.open-button {
  background-color: #834694;
  color: white;
  border-radius: 0.5rem;
  padding: 0.5rem;
  margin: 0.5rem;
  border: none;
  cursor: pointer;
}
</style>

<script setup lang="ts">
import { ref, computed, defineProps } from 'vue'
import { ImageInfo } from 'favicons-scraper'

export type IconListItemProps = {
  image: ImageInfo;
}

const props = defineProps<IconListItemProps>()

const iconStyle = computed(() => {
  return {
    height: `${Math.max(Math.min(Math.floor(props.image.size.height), 64), 32)}px`,
    width: `${Math.max(Math.min(Math.floor(props.image.size.width), 64), 32)}px`
  }
})

const expandedContent = ref<HTMLElement | null>(null)
const expanded = ref(false)
const expand = () => {
  expanded.value = !expanded.value
}

const expandedStyle = computed(() => {
  if (!expanded.value) return { height: `0px !important` }
  console.log('expanded', expanded.value)

  const children = expandedContent.value?.children
  if (!children) return { height: `0px` }
  console.log(children)

  let height = 0
  for (let i = 0; i < children.length; i++) {
    height += children[i].clientHeight
  }

  return { height: `${height}px` }
})

const openImage = () => {
  window.open(props.image.src, '_blank')
}
</script>