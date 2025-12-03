<template>
  <div id="app">
    <main>
      <MenuView v-if="activeTab === 'home'" @open="openTab" />
      <div v-if="activeTab === 'italie2'" class="scene">
        <MapView />
      </div>
    </main>
  </div>
</template>

<script>
import MenuView from './components/MenuView.vue'
import MapView from './components/MapView.vue'

export default {
  components: { MenuView, MapView },
  data() {
    return {
      activeTab: 'home'
    }
  },
  methods: {
    openTab(tab) {
      if (tab === 'italie2') {
        this.activeTab = 'italie2'
      } else {
        this.activeTab = 'home'
      }
    }
  }
}
</script>

<style scoped>
main { padding:0; min-height:100vh; }
</style>
