<template>
  <v-dialog width="350px" persistent v-model="editDialog">
    <v-btn fab accent slot="activator">
      <v-icon>edit</v-icon>
    </v-btn>
    <v-card>
      <v-container>
        <v-layout row wrap>
          <v-flex xs12>
            <v-card-title>Edit Profile</v-card-title>
          </v-flex>
        </v-layout>
        <v-divider></v-divider>
        <v-layout row wrap>
          <v-flex xs12>
            <v-card-text>
              <v-text-field
                name="name"
                label="Name"
                id="title"
                v-model="editedName"
                required></v-text-field>
              <v-text-field
                name="regno"
                label="Registration Number"
                id="regno"
                v-model="editedRegno"
                required></v-text-field>
              <v-text-field
                name="age"
                label="Age"
                id="age"
                v-model="editedAge"
                required></v-text-field>
              <v-text-field
                name="course"
                label="Course"
                id="course"
                v-model="editedCourse"
                required></v-text-field>
            </v-card-text>
          </v-flex>
        </v-layout>
        <v-divider></v-divider>
        <v-layout row wrap>
          <v-flex xs12>
            <v-card-actions>
              <v-btn
                flat
                class="blue--text darken-1"
                @click="editDialog = false">Close</v-btn>
              <v-btn flat class="blue--text darken-1" @click="onSaveChanges">Save</v-btn>
            </v-card-actions>
          </v-flex>
        </v-layout>
      </v-container>
    </v-card>
  </v-dialog>
</template>

<script>
  export default {
    props: ['meetup'],
    data () {
      return {
        editDialog: false,
        editedName: this.meetup.name,
        editedRegno: this.meetup.regno,
        editedAge: this.meetup.age,
        editedCourse: this.meetup.course,
      }
    },
    methods: {
      onSaveChanges () {
        if (this.editedName.trim() === '' || this.editedRegno.trim() === '') {
          return
        }
        this.editDialog = false
        this.$store.dispatch('updateMeetupData', {
          id: this.meetup.id,
          name: this.editedName,
          regno: this.editedRegno,
          age: this.editedAge,
          course: this.editedCourse,
        })
      }
    }
  }
</script>
