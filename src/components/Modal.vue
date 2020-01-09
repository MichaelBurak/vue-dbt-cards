<template>
  <v-row justify="center">
    <v-dialog v-model="modal" persistent max-width="290">
      <template v-slot:activator="{ on }">
        <v-list-item>
          <v-list-item-content>
            <v-row justify="center">
              <v-btn color="primary" dark v-on="on" @click="modal = true">About</v-btn>
            </v-row>
          </v-list-item-content>
        </v-list-item>
      </template>
      <v-card>
        <v-card-title class="headline">DBT-Cards-Vue</v-card-title>
        <v-card-text>
          This app was created by
          <a
            href="https://www.linkedin.com/in/michael-burak-99a58a105/"
          >Michael Burak</a>, who has benefited greatly from DBT and CBT practice over the years. A minimal implementation of diary cards, it is meant to be used and then printed out or screen captured, so there is no concern with user data being accessed. This limits functionality, but provides security. If you like this app, consider connecting on LinkedIn, Twitter, Github, or other platforms Michael is on, currently hunting for a good job with meaningful work.
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="modal = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    modal: false
  })
};
</script>