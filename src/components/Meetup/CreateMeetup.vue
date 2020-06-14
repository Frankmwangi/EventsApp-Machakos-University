<template>
  <v-container>
    <v-layout row>
      <v-flex xs12 sm6 offset-sm3>
             
        <h2 class="secondary--text">Create a new Profile</h2>
      </v-flex>
    </v-layout>
    <v-layout row>
      <v-flex xs12>
        <form @submit.prevent="onCreateMeetup">
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field
                name="name"
                label="Full Name"
                id="name"
                v-model="name"
                required></v-text-field>
            </v-flex>
          </v-layout>
            <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field
                name="course"
                label="Course"
                id="course"
                v-model="course"
                required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field
                name="RegNo"
                label="Registration Number"
                id="RegNo"
                v-model="regno"
                required></v-text-field>
            </v-flex>
          </v-layout>
           <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field
                name="Age"
                label="Age"
                id="Age"
                v-model="age"
                required></v-text-field>
            </v-flex>
          </v-layout>
           <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-btn raised class="primary" @click="onPickFile">Upload Your Image</v-btn>
              <input
                type="file"
                style="display: none"
                ref="fileInput"
                accept="image/*"
                @change="onFilePicked">
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <img :src="imageUrl" height="150">
            </v-flex>
          </v-layout>
         
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <h2 class="secondary--text">Choose admission Date & Time</h2>
            </v-flex>
          </v-layout>
          <v-layout row class="mb2">
            <v-flex xs12 sm6 offset-sm3>
              <v-date-picker v-model="date" 
                    :min="getToday"
                    class="mt-3"
            ></v-date-picker>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-time-picker v-model="time" format="24hr"></v-time-picker>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-btn
                class="primary"
                :disabled="!formIsValid"
                type="submit">Create Event</v-btn>
            </v-flex>
          </v-layout>
          </form>
          </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import Home from '../Home'
  export default {
    components: {
      Home
    },
    props: {
      items: {
        type: String
      },
      selected: {
       type: String
      }
    },
        data: () => ({
      items: ['Foo', 'Bar', 'Fizz', 'Buzz'],
    }),
    data () {
      return {
        course: '',
        name: '',
        regno: '',
        imageUrl: '',
        date: '',
        time: new Date(),
        image: '',
        age: ''
     
      }
    },
    
    computed: {
      formIsValid () {
        return this.name !== '' &&
        this.regno !== '' &&
        this.imageUrl !== '' &&
        this.date !== '' &&
        this.course !== ''&&
        this.age !== '' &&
        this.time !== ''
      },
      getToday () {
        let month = (new Date().getMonth() + 1)
        let day = (new Date().getDate() + 1)
        if (month < 10) {
          month = '0' + month
        }
        if (day < 10) {
          day = '0' + day
        }
        let dt = new Date().getFullYear() + '-' + month + '-' + day
        console.log(dt)
        return dt
      },
      submittableDateTime () {
        const date = new Date(this.date)
        if (typeof this.time === 'string') {
          let hours = this.time.match(/^(\d+)/)[1]
          const minutes = this.time.match(/:(\d+)/)[1]
          date.setHours(hours)
          date.setMinutes(minutes)
        } else {
          date.setHours(this.time.getHours())
          date.setMinutes(this.time.getMinutes())
        }
        return date
      }
    },
    methods: {
    
      allowedDates () {
        return '2019-05-23'
      },
      onCreateMeetup () {
        if (!this.formIsValid) {
          return
        }
        if (!this.image) {
          return
        }
        const meetupData = {
          name: this.name,
          regno: this.regno,
          image: this.image,
          imageUrl: this.imageUrl,
          date: this.submittableDateTime,
          course:this.course,
          age:this.age
        }
        
        this.$store.dispatch('createMeetup', meetupData)
        this.$router.push('/meetups')
        console.log(user.id)
      },
      onPickFile () {
        this.$refs.fileInput.click()
      },
      onFilePicked (event) {
        const files = event.target.files
        let filename = files[0].name
        console.log('filename: ', filename)
        if (filename.lastIndexOf('.') <= 0) {
          return alert('Please add a valid file!')
        }
        const fileReader = new FileReader()
        fileReader.addEventListener('load', () => {
          this.imageUrl = fileReader.result
        })
        fileReader.readAsDataURL(files[0])
        this.image = files[0]
      }
    }
  }
  
</script>
