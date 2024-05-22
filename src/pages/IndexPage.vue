<template>
  <q-page class="row items-start justify-center page-background q-pa-lg">
    <div class="col-12 row justify-center">
      <div class="col-12">
        <h1 class="page-header text-white text-weight-bolder text-center no-margin">Favicon Scraper</h1>
      </div>
      <div class="col-12 q-py-lg row justify-center">
        <text-input class="col-auto" v-model="url" label="URL" @update:model-value="handleUrlChange" placeholder="domain.com"/>
      </div>
      <div class="col-12 icon-list-container row q-pb-lg q-px-md justify-center">

        <div v-if="loading" class="q-pa-md text-center">
          <q-spinner-gears color="white" size="50px" />
        </div>

        <div v-else class="col-12 row justify-center">
          <div v-for="icon in logo" :key="icon.src" class="icon-list-item col-auto q-pa-md">
            <q-img :src="icon.src" fit="scale-down" alt="icon" class="icon" position="0% 100%" :width="`${icon.size.width.toString()}px`"/>
            <div class="icon-info">
              <p class="icon-info__size no-margin">Height: {{ icon.size.height }}px</p>
              <p class="icon-info__size no-margin ">Width: {{ icon.size.width }}px</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<style scoped lang="scss">
.page-background {
  background-image: linear-gradient(43deg, #E39EC1, #DEBAC0);
}
.icon-list-container {
  max-width: 1200px;
}
.page-header {
  text-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
}
</style>

<script setup lang="ts">
import { ref } from 'vue'
import TextInput from 'src/components/TextInput.vue';
import { getLogos, ImageInfo } from 'favicons-scraper'
import { Notify } from 'quasar';

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
