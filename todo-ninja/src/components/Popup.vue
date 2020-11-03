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
            <v-form class="px-3" ref="form">
                <v-text-field label="Title" v-model="title" prepend-icon="mdi-folder" :rules="inputRules"></v-text-field>
                <v-textarea label="Information" v-model="content" prepend-icon="mdi-pencil" :rules="inputRules"></v-textarea>
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
                      v-model="FormattedDate"
                      label="Due On"
                      prepend-icon="mdi-calendar"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                      :rules="inputRules"
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
                <v-btn class="mx-0 mt-3 white--text" color="#3cd1c2" @click="submit" :loading="loading">Add Project</v-btn>
            </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>
</template>

<script>
import { format } from 'date-fns'
import parseISO from 'date-fns/parseISO'
import db from '@/fb'

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
      inputRules: [
        v => v.length >= 3 || 'Minimum length is 3 characters'
      ],
      loading: false
    }
  },
  methods: {
    submit(){
      if(this.$refs.form.validate()){
        this.loading = true
        const project = {
          title: this.title, 
          content: this.content,
          due: format(parseISO(this.due), 'do MMM yyyy'),
          person: 'The Net Ninja',
          status: 'ongoing'
        }
        db.collection('projects').add(project).then(() => {
          this.loading = false
          this.dialog = false
          this.$emit('projectAdded')
        })
      }
    },
  },
  computed: {
    FormattedDate () {
      return this.due ? format(parseISO(this.due), 'do MMM yyyy') : ''
    },
  },
}
</script>