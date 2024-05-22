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
// .text-input {
//   width: 100%;
//   padding: 10px;
//   font-size: 1.5rem;
//   border: 1px solid #ccc;
//   border-radius: 5px;
//   box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
// }
</style>

<script lang="ts" setup>
import { defineModel, defineProps } from 'vue'

interface TextInputProps {
  placeholder: string
}

const props = defineProps<TextInputProps>()

const model = defineModel()

</script>