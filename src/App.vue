<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center"></div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content id="content">
      <!-- <ImageMaker /> -->
      <DbtCard />
    </v-content>
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
