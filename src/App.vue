<template>
  <TheHeader title="RemeberMe" />
  <TheResources />
</template>

<script>
  import TheResources from './components/learning-resources/TheResources'
  import TheHeader from './components/layout/TheHeader'

  export default {
    components: {
      TheResources,
      TheHeader,
    },
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

  * {
    box-sizing: border-box;
  }

  html {
    font-family: 'Roboto', sans-serif;
  }

  body {
    margin: 0;
  }
</style>
