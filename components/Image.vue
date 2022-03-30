<template>
  <div :style="containerStyle">

    <ve-image src="wc:Boy_and_book_by_Charles_Porter.jpg"></ve-image>

  </div>  
</template>

<script>

module.exports = {
  name: 've-image',
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
    containerStyle() { return { height: this.viewerIsActive ? '100%' : '0' } }
  },
  mounted() { this.loadDependencies(this.dependencies, 0, this.init) },
  methods: {
    init() {
      console.log(`${this.$options.name}.mounted`, this.items)
    }
  }
}

</script>

<style>
</style>
