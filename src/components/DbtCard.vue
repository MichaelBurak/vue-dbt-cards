<template>
  <v-container fluid>
    <div>
      <Modal />
      <v-divider />

      <v-row justify="center">
        <v-card class="mx-auto" outlined>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="overline mb-4" justify="right">HOW TO USE</div>
              <v-list-item-title class="headline mb-1">Fill out and print!</v-list-item-title>
              <v-list-item-subtitle>None of your data is saved, take a screenshot or print to PDF to keep your DBT cards.</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </v-row>
      <v-divider />
      <v-row justify="center">
        <v-date-picker v-model="picker" show-week></v-date-picker>
      </v-row>
      <v-divider />
      <v-row justify="center" dense>
        <v-card class="mx-auto" outlined>
          <v-text-field v-model="firstname" label="Name" required></v-text-field>
        </v-card>
      </v-row>

      <v-divider />
      <v-divider />
      <v-data-table :headers="headers" :items="fields" class="elevation-1" hide-default-footer>
        <template v-slot:top>
          <v-dialog v-model="dialog" max-width="500px">
            <template v-slot:activator="{ on }"></template>
            <v-card height="50%" class="m-y-4 mx-lg-auto">
              <v-card-title>
                <span class="headline">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.use" label="Use(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.suicide" label="Suicide(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.sh" label="S-H(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.pain" label="Pain(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.sad" label="Sadness(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.shame" label="Shame(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.anger" label="Anger(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.fear" label="Fear(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.joy" label="Joy(0-5)"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.skills" label="Skills Usage(0-5)"></v-text-field>
                  </v-col>
                </v-row>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
                <v-btn color="blue darken-1" text @click="save">Save</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </template>
        <template v-slot:item.action="{ item }">
          <v-icon small class="mr-2" @click="editItem(item)">fas fa-edit</v-icon>
        </template>
        <template v-slot:no-data>
          <v-btn color="primary" @click="initialize">Reset</v-btn>
        </template>
      </v-data-table>
      <v-divider />

      <Ub />
      <v-divider />

      <v-row justify="left">
        <v-col cols="12" md="3">
          <v-card>
            <v-textarea
              outlined
              name="input-7-4"
              label="Notes"
              value="Enter notes for the week here."
            ></v-textarea>
          </v-card>
        </v-col>
      </v-row>
      <Radical />
    </div>
  </v-container>
</template>



<script>
import Ub from "./Ub";
import Modal from "./Modal";
import Radical from "./Radical";
export default {
  data: () => ({
    dialog: false,
    rModal: false,
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
    Ub,
    Modal,
    Radical
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
    },
    openRModal() {
      this.rModal = true;
    }
  }
};
</script>
