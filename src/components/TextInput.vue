<template>
  <div class="row q-col-gutter-x-sm">
    <div class="col-auto self-center">
      <q-icon name="search" size="2rem"/>
    </div>
    <input type="text" class="text-input col" v-model="model" :placeholder="placeholder"/>
  </div>
</template>

<style scoped lang="scss">
.text-input {
  background-color: transparent;
  border: none;
  color: inherit;
  font-size: 1.5rem;
}
.text-input:focus {
  outline: none;
}
</style>

<script lang="ts" setup>
import { defineModel, defineProps } from 'vue'

interface TextInputProps {
  placeholder: string
}

const props = defineProps<TextInputProps>()

const model = defineModel()
</script>