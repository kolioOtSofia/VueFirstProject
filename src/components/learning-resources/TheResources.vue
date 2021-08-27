<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')"
    :mode="selectedTab === 'stored-resources' ? null : 'flat'"
      >Stored Resources</base-button
    >
    <base-button @click="setSelectedTab('add-resource')"
    :mode="selectedTab === 'add-resource' ? null : 'flat'"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },

  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'Google',
          title: 'Google',
          description: 'The most popular search engine',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
      return {
          resources: this.storedResources,
          addResource: this.addResource,
          removeResource: this.removeResource
      }
  },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    
    addResource(title, desc, enteredUrl) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: desc,
        link: enteredUrl
      }
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },

    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id = resId);
      this.storedResources.splice(resIndex, 1);
    }
  },
};
</script>