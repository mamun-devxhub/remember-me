<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      >Add Resource</base-button
    >
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </base-card>
</template>

<script>
import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue";

export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: "stored-resources",
      resources: [
        {
          id: "vuejs-official",
          title: "Official Guide",
          description: "The official Vue.js documentation",
          link: "https://vuejs.org",
        },
        {
          id: "google",
          title: "Google",
          description: "Learn Goooooooogle",
          link: "https://google.com",
        },
      ],
    };
  },

  provide() {
    return {
      resources: this.resources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
    };
  },

  computed: {
    storedResButtonMode() {
      return this.selectedTab === "stored-resources" ? null : "flat";
    },
    addResButtonMode() {
      return this.selectedTab === "add-resource" ? null : "flat";
    },
  },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },

    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };
      this.resources.unshift(newResource);
      this.selectedTab = "stored-resources";
    },

    removeResource(resId) {
      // this.resources = this.resources.filter((res) => res.id !== resId);
      const resIndex = this.resources.findIndex((res) => res.id === resId);
      this.resources.splice(resIndex, 1);

      console.log(this.resources.length);
    },
  },
};
</script>

<style>
</style>