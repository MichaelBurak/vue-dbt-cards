<template>
  <!-- <div> -->
  <v-row justify="left" class="mx-lg-auto">
    <v-data-table :headers="ubHeaders" :items="ub" class="elevation-1" hide-default-footer>
      <template v-slot:top>
        <v-toolbar flat color="white">
          <v-toolbar-title>Urges and Beliefs</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="500px">
            <template v-slot:activator="{ on }"></template>
            <v-card>
              <v-card-title>
                <span class="headline">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.before" label="Before"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.after" label="After"></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
                <v-btn color="blue darken-1" text @click="save">Save</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:item.action="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)">fas fa-edit</v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize">Reset</v-btn>
      </template>
    </v-data-table>
  </v-row>
  <!-- </div> -->
</template>



<script>
export default {
  data: () => ({
    dialog: false,
    ubHeaders: [
      {
        text: "Statuses",
        align: "left",
        sortable: false,
        value: "name"
      },
      { text: "Before", value: "before" },
      { text: "After", value: "after" },
      { text: "Actions", value: "action", sortable: false }
    ],
    ub: [
      {
        name: "Urge to Use"
      },
      { name: "Urge to Quit Therapy" },
      { name: "Urge to Harm" },
      { name: "Belief in control of Emotions" },
      { name: "Belief in control of Behaviors" },
      { name: "Belief in control of Thoughts" }
    ],
    editedIndex: -1,
    editedItem: {
      before: "",
      after: ""
    },
    defaultItem: {
      before: "",
      after: ""
    }
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    }
  },

  watch: {
    dialog(val) {
      val || this.close();
    }
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.ub = [
        {
          name: "Urge to Use"
        },
        { name: "Urge to Quit Therapy" },
        { name: "Urge to Harm" },
        { name: "Belief in control of Emotions" },
        { name: "Belief in control of Behaviors" },
        { name: "Belief in control of Thoughts" }
      ];
    },

    editItem(item) {
      debugger;
      this.editedIndex = this.ub.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    close() {
      this.dialog = false;
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      }, 300);
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.ub[this.editedIndex], this.editedItem);
      } else {
        this.ub.push(this.editedItem);
      }
      this.close();
    }
  }
};
</script>
