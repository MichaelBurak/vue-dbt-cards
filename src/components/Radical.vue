<template>
  <v-row>
    <v-card>
      <v-toolbar flat color="primary" dark>
        <v-toolbar-title>Exercises</v-toolbar-title>
      </v-toolbar>
      <v-tabs vertical>
        <v-tab>
          <v-icon left @click="rModal = true">mdi-account</v-icon>Radical Acceptance
        </v-tab>
        <v-tab>
          <v-icon left>mdi-account</v-icon>Emotional Identification
        </v-tab>

        <v-tab-item>
          <v-card flat>
            <v-card-text>
              <p>For identifying and working through a situation you're struggling to accept.</p>

              <p>For identifying the function of an emotion you've experienced.</p>
            </v-card-text>
          </v-card>
        </v-tab-item>
        <v-tab-item></v-tab-item>
      </v-tabs>
    </v-card>
    <v-dialog v-model="rModal" persistent max-width="290">
      <template v-slot:activator="{ on }">
        <v-list-item>
          <v-list-item-content>
            <v-row>
              <v-btn color="primary" dark v-on="on">Radical Acceptance Exercise</v-btn>
            </v-row>
          </v-list-item-content>
        </v-list-item>
      </template>
      <v-card>
        <v-card-title class="headline">Radical Acceptance</v-card-title>
        <v-card-text>What is the situation you are trying to accept?</v-card-text>
        <v-spacer />
        <v-textarea outlined name="input-7-4" label="Situation" />
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text @click="difficultyModal = true">Next Step</v-btn>
          <v-btn color="green darken-1" text @click="rModal = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-row>
      <v-dialog v-model="difficultyModal" persistent max-width="290">
        <template v-slot:activator="{ on }"></template>
        <v-card>
          <v-card-title class="headline">Radical Acceptance</v-card-title>
          <v-card-text>What is the difficult part of the situation you are trying to accept?</v-card-text>
          <v-spacer />
          <v-textarea outlined name="input-7-4" label="Difficulty" />
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn text @click="finalModal = true">Next Step</v-btn>
            <v-btn color="green darken-1" text @click="difficultyModal = false">Close</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>
    <v-row>
      <v-dialog v-model="finalModal" persistent max-width="290">
        <template v-slot:activator="{ on }"></template>
        <v-card>
          <v-card-title class="headline">Radical Acceptance</v-card-title>
          <v-card-text>What is the reality of the situation you are trying to accept?</v-card-text>
          <v-spacer />
          <v-textarea outlined name="input-7-4" label="Reality" />
          <v-card-actions>
            <v-spacer></v-spacer>

            <v-btn
              color="green darken-1"
              text
              @click="finalModal = false,difficultyModal=false,rModal=false "
            >Accept and Close</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>
  </v-row>
</template>

<script>
export default {
  //   props: {
  //     source: String
  //   },
  data: () => ({
    rModal: false,
    difficultyModal: false,
    finalModal: false
  })
};
</script>