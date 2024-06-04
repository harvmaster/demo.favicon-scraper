<template>
  <q-layout view="lHh Lpr lFf" class="page-background">
    <!-- <q-header elevated style="background-color: #2F323A">
      <q-toolbar class="bg-transparent">
        <h6 class="no-margin">Favicons Scraper</h6>
      </q-toolbar>
    </q-header> -->

    <q-page-container>
      <router-view />
    </q-page-container>


    <q-footer unelevated style="background-color: transparent">
      <q-toolbar class="bg-transparent">
        <q-space />
        <q-btn
          icon="img:/icons/github_icon.svg"
          outlined
          color="grey-8"
          round
          @click="openSource"
        />
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<style scoped lang="scss">
.page-background {
  background-color: rgb(21, 21, 21);
}
</style>

<script setup lang="ts">
const openSource = () => {
  window.open('https://github.com/harvmaster/demo.favicon-scraper', '_blank')
}
</script>
