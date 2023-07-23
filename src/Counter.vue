<script setup>
import {reactive} from "vue";

const state = reactive({count: 0})

const setCount = () => {
  state.count++
}
</script>
<template>
  <div>
    <button @click="setCount">{{ state.count}}</button>
  </div>
</template>