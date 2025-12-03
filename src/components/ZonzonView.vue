<template>
  <div class="zonzon-container">
    <div id="zonzon-map" class="map-canvas"></div>
    <div class="map-title">zonzon</div>
    <div class="projection-info">Projection: Equal Earth (vraies proportions)</div>
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl'

export default {
  name: 'ZonzonView',
  mounted() {
    this.initMap()
  },
  methods: {
    initMap() {
      mapboxgl.accessToken = import.meta.env.VITE_MAPBOX_TOKEN
      
      this.map = new mapboxgl.Map({
        container: 'zonzon-map',
        style: 'mapbox://styles/mapbox/satellite-streets-v12',
        projection: 'equalEarth', // Projection qui respecte les vraies tailles
        center: [0, 20],
        zoom: 1.5
      })

      this.map.addControl(new mapboxgl.NavigationControl(), 'top-right')
    }
  },
  beforeUnmount() {
    if (this.map) {
      this.map.remove()
    }
  }
}
</script>

<style scoped>
.zonzon-container {
  position: relative;
  width: 100%;
  height: 100vh;
  background: #000;
}

.map-canvas {
  width: 100%;
  height: 100%;
}

.map-title {
  position: absolute;
  top: 20px;
  left: 20px;
  background: rgba(0, 0, 0, 0.85);
  padding: 12px 24px;
  border-radius: 8px;
  font-size: 20px;
  font-weight: bold;
  color: #fff;
  box-shadow: 0 2px 8px rgba(0,0,0,0.3);
  z-index: 1;
}

.projection-info {
  position: absolute;
  bottom: 30px;
  left: 20px;
  background: rgba(0, 0, 0, 0.75);
  padding: 8px 16px;
  border-radius: 6px;
  font-size: 13px;
  color: #fff;
  z-index: 1;
}
</style>
