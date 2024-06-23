<template>
    <v-container>
      <Map
        name="Goblin Cave"
        imageSrc="@/assets/goblin.png"
        :startTime="0"
      />
      <Map
        name="Ice Cavern"
        imageSrc="@/assets/frost.png"
        :startTime="180" 
      />
      <Map
        name="Forgotten Castle"
        imageSrc="@/assets/castle.png"
        :startTime="360"
      />
    </v-container>
  </template>
  
  <script setup lang="ts">
  import Map from './Map.vue';
  </script>
  
  <style scoped>
  </style>
  