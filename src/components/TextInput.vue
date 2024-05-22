<template>
  <div class="">
    <input type="text" class="text-input" v-model="model" :placeholder="placeholder"/>
  </div>
</template>

<style scoped lang="scss">
.text-input {
  width: 100%;
  padding: 10px;
  font-size: 1.5rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
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