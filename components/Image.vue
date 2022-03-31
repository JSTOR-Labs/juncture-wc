<template>
  <div :style="containerStyle">

    <ve-image>
      <ul>
        <li v-for="(manifestUrl, idx) in manifestUrls" :key="idx">{{manifestUrl}}</li>
      </ul>
    </ve-image>

  </div>  
</template>

<script>

module.exports = {
  name: 've2-image',
  props: {
    items: { type: Array, default: () => ([]) },
    viewerIsActive: Boolean
  },
  data: () => ({
    viewerLabel: 'Image Web Component',
    viewerIcon: 'fas fa-code',
    dependencies: []
  }),
  computed: {
    containerStyle() { return { height: this.viewerIsActive ? '100%' : '0' } },
    viewerItems() { return this.items.filter(item => item.viewer === 've-image') },
    manifestUrls() {
      return this.viewerItems.map(item => {
        return item.manifest || item.src
          ? item.manifest || item.src
          : `/${item.url}`
      })
    }
  },
  mounted() { this.loadDependencies(this.dependencies, 0, this.init) },
  methods: {
    init() {
      console.log(`${this.$options.name}.mounted`, this.items, this.viewerItems)
    }
  },
  watch: {
    items (current) {
      console.log('watch.items', current)
    },
    manifestUrls (current) {
      console.log('watch.manifestUrls', current)
    }
  }
}

</script>

<style>
</style>
