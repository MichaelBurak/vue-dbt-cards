<template>
  <div>
    <v-data-table :headers="headers" :items="fields" class="elevation-1">
      <template v-slot:top>
        <v-toolbar flat color="white">
          <v-toolbar-title>Vue DBT Cards</v-toolbar-title>
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
                      <v-text-field v-model="editedItem.use" label="Use"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.suicide" label="Suicide"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.sh" label="S-H"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.pain" label="Pain"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.sad" label="Sadness"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.shame" label="Shame"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.anger" label="Anger"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.fear" label="Fear"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.joy" label="Joy"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field v-model="editedItem.skills" label="Skills"></v-text-field>
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
        <v-icon small class="mr-2" @click="editItem(item)">edit</v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize">Reset</v-btn>
      </template>
    </v-data-table>

    <Broken />
  </div>
</template>



<script>
import Broken from "./Broken";
export default {
  data: () => ({
    dialog: false,
    headers: [
      {
        text: "Day and Date",
        align: "left",
        sortable: false,
        value: "name"
      },
      { text: "Use", value: "use" },
      { text: "Suicide", value: "suicide" },
      { text: "S-H", value: "sh" },
      { text: "Pain", value: "pain" },
      { text: "Sadness", value: "sad" },
      { text: "Shame", value: "shame" },
      { text: "Anger", value: "anger" },
      { text: "Fear", value: "fear" },
      { text: "Joy", value: "joy" },
      { text: "Skills", value: "skills" },
      { text: "Actions", value: "action", sortable: false }
    ],
    fields: [
      {
        name: "Mon"
      },
      { name: "Tues" },
      { name: "Wed" },
      { name: "Thur" },
      { name: "Fri" },
      { name: "Sat" },
      { name: "Sun" }
    ],
    editedIndex: -1,
    editedItem: {
      use: "",
      suicide: "",
      sh: "",
      pain: "",
      sadness: "",
      shame: "",
      anger: "",
      fear: "",
      joy: "",
      skills: ""
    },
    defaultItem: {
      use: "",
      suicide: "",
      sh: "",
      pain: "",
      sadness: "",
      shame: "",
      anger: "",
      fear: "",
      joy: "",
      skills: ""
    }
  }),
  components: {
    Broken
  },

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
      this.fields = [
        {
          name: "Mon"
        },
        { name: "Tues" },
        { name: "Wed" },
        { name: "Thur" },
        { name: "Fri" },
        { name: "Sat" },
        { name: "Sun" }
      ];
    },

    editItem(item) {
      debugger;
      this.editedIndex = this.fields.indexOf(item);
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
        Object.assign(this.fields[this.editedIndex], this.editedItem);
      } else {
        this.fields.push(this.editedItem);
      }
      this.close();
    }
  }
};
</script>
