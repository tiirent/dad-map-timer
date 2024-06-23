<template>
  <v-container class="fill-height">
    <v-responsive
      class="align-centerfill-height mx-auto"
      max-width="900"
    >
      <Header />
      <Map
        name="Goblin Cave"
        imageSrc="@/assets/goblin.png"
        :startTime="0"
      />
      <Map
        name="Forgotten Castle"
        imageSrc="@/assets/castle.png"
        :startTime="360"
      />
      <Map
        name="Frost Mountain"
        imageSrc="@/assets/frost.png"
        :startTime="180" 
      />
      <v-row align="end" justify="center">
        <div class="text-h6 ma-2">*If times are out of sync please refresh</div>
      </v-row>
    </v-responsive>
  </v-container>
  </template>
  
  <script setup lang="ts">
  import Map from './Map.vue';
  import Header from './Header.vue';
  </script>
  
  <style scoped>
  </style>
  