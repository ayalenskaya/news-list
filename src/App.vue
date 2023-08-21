<template>
  <news-list/>
</template>

<script>
import NewsList from '@/components/NewsList.vue'

export default {
  name: 'App',
  components: {
    NewsList
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito+Sans:opsz,wght@6..12,400;6..12,700&display=swap');

* {
  box-sizing: border-box;
  outline: none;
}

html,
body {
  min-height: 100%;
  margin: 0;
  font-family: Nunito Sans;
}
</style>
