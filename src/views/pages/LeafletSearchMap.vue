<template>
    <div>
      <div id="map"></div>
      <div>
        Latitude: <input type="text" v-model="lat">
        Longitude: <input type="text" v-model="lng">
        Alamat: <input type="text">
      </div>
    </div>
  </template>
  
  <script>
  import L from 'leaflet';
  
  export default {
    data() {
      return {
        map: null,
        lat: '',
        lng: '',
        marker: null
      };
    },
    methods: {
      addMarker(latLng) {
        // Remove the previous marker, if any
        if (this.marker) this.map.removeLayer(this.marker);
        
        // Add a new marker to the map
        this.marker = L.marker([latLng.lat, latLng.lng]).addTo(this.map);
      }
    },
    mounted() {
      this.map = L.map('map').setView([-6.905977, 107.613144], 13);
  
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: 'Map data © <a href="https://openstreetmap.org">OpenStreetMap</a> contributors',
      }).addTo(this.map);
  
      this.map.on('click', (e) => {
        const latLng = e.latlng;
        this.lat = latLng.lat.toFixed(6);
        this.lng = latLng.lng.toFixed(6);
        
        this.addMarker(latLng);
      });
    },
  };
  </script>
  
  <style>
  #map {
    width: 100%;
    height: 580px;
  }
  </style>
  