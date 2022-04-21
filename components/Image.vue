<template>
  <div :style="containerStyle">

    <ve-image :user="user" :path="path">
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
    contentSource:  { type: Object, default: () => ({}) },
    viewerIsActive: Boolean
  },
  data: () => ({
    viewerLabel: 'Image Viewer',
    viewerIcon: 'far fa-file-image',
    dependencies: []
  }),
  computed: {
    containerStyle() { return { height: this.viewerIsActive ? '100%' : '0' } },
    viewerItems() { return this.items.filter(item => item.viewer === 've-image') },
    manifestUrls() { return this.viewerItems.map(item => item.manifest || item.src ? item.manifest || item.src : `/${item.url}`) },
    user() { return this.contentSource.acct },
    path() { 
      let pathElems = this.contentSource.basePath.split('/').filter(elem => elem)
      return pathElems.slice(this.contentSource.isGhpSite ? 2 : 1).join('/')
    }
  },
  mounted() {
    console.log('contentSource', this.contentSource)
    console.log(`user=${this.user} path=${this.path}`)
    this.loadDependencies(this.dependencies, 0, this.init)
  },
  methods: {
    init() { console.log(`${this.$options.name} initialized`) }
  }
}

</script>

<style>
</style>
