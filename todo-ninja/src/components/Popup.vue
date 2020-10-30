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
                <v-text-field label="Title"></v-text-field>
            </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>
</template>