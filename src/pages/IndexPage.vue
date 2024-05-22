<template>
  <q-page class="row items-center justify-center page-background q-pa-lg">
    <div class="col-auto page-content justify-center">
      <div class="col-auto full-width row q-pa-sm justify-center">
        <text-input class="col-12" v-model="url" label="URL" @update:model-value="handleUrlChange" placeholder="domain.com"/>
      </div>

      <div v-if="logo.length" class="col-auto full-width q-px-md">
        <q-separator style="background-color: #8e8e8e" />
      </div>

      <div class="col-auto full-width" :class="logo.length && 'q-pa-md'">
        <icon-list class="icon-list" :images="logo"/>
      </div>
    </div>
  </q-page>
</template>

<style scoped lang="scss">
.page-content {
  width: 900px;
  max-height: 90vh;
  overflow: scroll;
  border-radius: 1em;
  background-color: #3e3e3e;
  border: 1px solid #8e8e8e;

  color: #9e9e9e;
}

.page-background {
  background-color: rgb(21, 21, 21);
}
.icon-list-container {
  max-width: 1200px;
}
.page-header {
  text-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
}
</style>

<script setup lang="ts">
import { computed, ref, watch, nextTick } from 'vue'
import TextInput from 'src/components/TextInput.vue';
import { getLogos, ImageInfo } from 'favicons-scraper'
import { Notify } from 'quasar';

import IconList from 'src/components/IconList/IconList.vue'

const loading = ref(false)

const url = ref('')
const logo = ref<ImageInfo[]>([])

const debounceTimer = ref<NodeJS.Timeout | null>(null)
const handleUrlChange = (value: string) => {
  // Clear old timer then create a new timer
  if (debounceTimer.value) clearTimeout(debounceTimer.value)
  debounceTimer.value = setTimeout(() => {
    getLogosFromUrl(url.value)
  }, 500)

  url.value = value
}

const getLogosFromUrl = async (urlInput: string) => {
  loading.value = true
  try {
    const logos = await getLogos(urlInput)
    console.log(urlInput, logos)
    if (url.value == urlInput) {
      logo.value = logos.sort((a, b) => a.size.width - b.size.width)
    }
  } catch (error) {
    console.log(url.value)
    if (url.value == '') {
      logo.value = []
      return
    }
    if (url.value == urlInput) {
      logo.value = []
      Notify.create({
        message: 'Error fetching logos',
        color: 'negative',
        position: 'top-right',
      })
    }

    console.error(error)
  } finally {
    loading.value = false
  }
}
</script>
