<template>
  <v-app>
    <v-app-bar app color="primary" dark dense>
      <div class="d-flex align-center"></div>

      <v-toolbar-title justify="center">Vue DBT Cards</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content id="content">
      <DbtCard />
    </v-content>
    <v-footer app color="primary" dark dense />
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
