<template>
  <router-view />
</template>

<script>
import { RouterView } from 'vue-router'

export default {
  name: 'App',
  components: {
    RouterView
  }
}
</script>

<style lang="scss">
@import '~@/../mdb/scss/index.free.scss';

#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
}
</style>
