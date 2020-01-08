<template>
  <v-app>
    <v-app-bar app color="primary" dark dense>
      <div class="d-flex align-center"></div>

      <v-toolbar-title justify="center">Vue DBT Cards</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>
    <!-- <v-container fluid> -->
    <v-content id="content">
      <!-- <ImageMaker /> -->
      <DbtCard />
    </v-content>
    <!-- </v-container> -->
  </v-app>
</template>

<script>
import DbtCard from "./components/DbtCard";
import ImageMaker from "./components/ImageMaker";

export default {
  name: "App",

  components: {
    DbtCard,
    ImageMaker
  },

  data: () => ({
    resetToggle: false
  })
};
</script>
