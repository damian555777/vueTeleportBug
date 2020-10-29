<template>
  <ul>
    <LearningResource
      v-for="resource in resources"
      v-bind:key="resource.id"
      v-bind:id="resource.id"
      v-bind:title="resource.title"
      v-bind:description="resource.description"
      v-bind:link="resource.link"
    />
  </ul>
</template>

<script>
  import LearningResource from './LearningResource'
  export default {
    components: {
      LearningResource,
    },
    inject: ['resources'],
  }
</script>

<style scoped>
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
    margin: auto;
    max-width: 40rem;
  }
</style>
