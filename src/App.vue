<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
    width: 100vw;
    height: 100vh;
    color: #ffffff;
    position: relative;
    overflow: hidden;
}
</style>
<style lang="sass">
@import './assets/css/custom.sass'
</style>
