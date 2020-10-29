<template>
  <BaseCard>
    <BaseButton
      v-on:click="setSelectedTab('StoredResources')"
      v-bind:mode="storedResButtonMode"
    >
      Stored Resources
    </BaseButton>
    <BaseButton
      v-on:click="setSelectedTab('AddResource')"
      v-bind:mode="addResButtonMode"
    >
      Add Resource
    </BaseButton>
  </BaseCard>
  <keep-alive>
    <component v-bind:is="selectedTab"></component>
  </keep-alive>
</template>

<script>
  import BaseCard from '../UI/BaseCard'
  import BaseButton from '../UI/BaseButton'

  import StoredResources from '../learning-resources/StoredResources'
  import AddResource from '../learning-resources/AddResource'

  export default {
    components: {
      BaseCard,
      BaseButton,
      StoredResources,
      AddResource,
    },
    data() {
      return {
        selectedTab: 'StoredResources',
        storedResources: [
          {
            id: 'official-guide',
            title: 'Official Guide',
            description: 'The official Vue.js documentation',
            link: 'https://vuejs.org',
          },
          {
            id: 'google',
            title: 'Google',
            description: 'Learn to Google...',
            link: 'https://google.com',
          },
        ],
      }
    },
    computed: {
      storedResButtonMode() {
        return this.selectedTab === 'StoredResources' ? '' : 'flat'
      },
      addResButtonMode() {
        return this.selectedTab === 'AddResource' ? '' : 'flat'
      },
      getResources() {
        return this.storedResources
      },
    },
    provide() {
      return {
        resources: this.getResources,
        addResource: this.addResource,
        deleteResource: this.deleteResource,
      }
    },
    methods: {
      setSelectedTab(tab) {
        this.selectedTab = tab
      },
      addResource(title, description, link) {
        this.storedResources.unshift({
          id: new Date().toISOString(),
          title,
          description,
          link,
        })
      },
      deleteResource(id) {
        if (id) {
          console.log({ id })
          const resourceIndex = this.storedResources.findIndex((resource) => {
            return resource.id === id
          })
          this.storedResources.splice(resourceIndex, 1)
        }
      },
    },
  }
</script>
