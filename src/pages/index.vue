<template>
  <v-app>
    <v-main>
      <Navbar />
      <Topcontents />

      <v-container fluid id="ygar">
        <v-row>
          <v-col>
            <Yourgarage />
            <Popularcars />
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" lg="6" md="6" sm="12">
            <Sellcar />
          </v-col>
          <v-col cols="12" lg="6" md="6" sm="12">
            <Researchcar />
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <Carsearch />
          </v-col>
        </v-row>
        <br><br>
        <Footer />
      </v-container>

      <Ai v-if="!hideAi" />
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from 'vue';
import Navbar from '@/components/Navbar.vue';
import Topcontents from '@/components/Topcontents.vue';
import Carsearch from '@/layouts/Carsearch.vue';
import Footer from '@/layouts/Footer.vue';
import Popularcars from '@/layouts/Popularcars.vue';
import Researchcar from '@/layouts/Researchcar.vue';
import Sellcar from '@/layouts/Sellcar.vue';
import Yourgarage from '@/layouts/Yourgarage.vue';
import Ai from '../layouts/Ai.vue';

const hideAi = ref(true); // Set this to true to hide the AI component.
</script>

<style scoped>
#ygar {
  background-color: #151515;
  position: absolute;
  z-index: 555;
}
</style>
