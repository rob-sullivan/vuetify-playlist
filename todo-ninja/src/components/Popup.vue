<template>
    <v-dialog
      v-model="dialog"
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
            color="#3cd1c2"
            dark
            v-bind="attrs"
            v-on="on"
        >
            Add new project
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="headline grey lighten-2">
          Add new project
        </v-card-title>
        <v-card-text>
            <v-form class="px-3">
                <v-text-field label="Title" v-model="title" prepend-icon="mdi-folder"></v-text-field>
                <v-textarea label="Information" v-model="content" prepend-icon="mdi-pencil"></v-textarea>
                <!-- Date picker -->
                <v-dialog
                  ref="dialog"
                  v-model="modal"
                  :return-value.sync="due"
                  persistent
                  width="290px"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="due"
                      label="Due On"
                      prepend-icon="mdi-calendar"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="due"
                    scrollable
                  >
                    <v-spacer></v-spacer>
                    <v-btn
                      text
                      color="primary"
                      @click="modal = false"
                    >
                      Cancel
                    </v-btn>
                    <v-btn
                      text
                      color="primary"
                      @click="$refs.dialog.save(due)"
                    >
                      OK
                    </v-btn>
                  </v-date-picker>
                </v-dialog>
                <v-btn class="mx-0 mt-3 white--text" color="#3cd1c2" @click="submit">Add Project</v-btn>
            </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>
</template>

<script>
import { format, parseISO } from 'date-fns'

export default {
  data(){
    return{
      title: '',
      content: '',
      due: new Date().toISOString().substr(0, 10),
      dialog: null,
      menu: false,
      modal: false,
      menu2: false,
    }
  },
  methods: {
    submit(){
      console.log(this.title, this.content, this.date)
    },
  },
  computed: {
    FormattedDate () {
      return this.date ? format(this.date, 'Do, MMM YYYY') : ''
    },
  },
}
</script>