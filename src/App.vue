<script setup>
import CompareImage from '@/views/CompareImage.vue';
import TheWelcome from './components/TheWelcome.vue'

const scale = ref('1:1')

function changeScale(scaleText) {
  scale.value = scaleText
}

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125"/>

    <div class="wrapper">
      <!--      <div class="flow">
              <n-button @click="changeScale('1:1')">1:1</n-button>
              <n-button @click="changeScale('1:2')">1:2</n-button>
              <n-button @click="changeScale('3:4')">3:4</n-button>
              <n-button @click="changeScale('9:16')">9:16</n-button>
              <n-button @click="changeScale('16:9')">16:9</n-button>
              <n-button @click="changeScale('4:3')">4:3</n-button>
            </div>-->
      <CompareImage/>
    </div>
  </header>

  <main>
    <TheWelcome/>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
