<template>
  <div class="map-view-container">
    <button class="back-button" @click="$emit('back')" title="Retour à l'accueil">← Accueil</button>
    <div id="italie2-map" class="map-canvas"></div>
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl'

export default {
  name: 'MapView',
  data() {
    return {
      map: null
    }
  },
  mounted() {
    this.initMap()
  },
  methods: {
    initMap() {
      mapboxgl.accessToken = import.meta.env.VITE_MAPBOX_TOKEN
      
      this.map = new mapboxgl.Map({
        container: 'italie2-map',
        style: 'mapbox://styles/mapbox/streets-v12',
        center: [2.3522, 48.8566], // Paris par défaut
        zoom: 12
      })

      this.map.addControl(new mapboxgl.NavigationControl(), 'top-right')
      this.map.addControl(new mapboxgl.ScaleControl({ unit: 'metric' }), 'bottom-left')
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
.map-view-container {
  position: relative;
  width: 100%;
  height: 100vh;
}

.map-canvas {
  width: 100%;
  height: 100%;
}

.back-button {
  position: absolute;
  top: 20px;
  right: 20px;
  background: rgba(255, 255, 255, 0.95);
  border: none;
  padding: 10px 20px;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0,0,0,0.15);
  z-index: 10;
  transition: all 0.3s ease;
}

.back-button:hover {
  background: #fff;
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  transform: translateY(-2px);
}
</style>
