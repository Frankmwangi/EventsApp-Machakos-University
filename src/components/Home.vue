<template>
  <v-container class="Home">
    <header class= "header">
      <div class="header__text-box">
                <h1 class="heading-primary">
                    <span class="heading-primary--main">WELCOME TO OUR REGISTRATION PORTAL</span>
                  </h1>

                  <v-btn
                class="primary"
                
                @click.prevent="submitCourse()"
                type="submit">REGISTER HERE</v-btn>
            </div>
    </header>
      
      <!-- <v-flex xs12 sm6 class="text-xs-center text-sm-right">
        <v-btn large router to="/meetups" class="secondary radius">View Profile</v-btn>
      </v-flex>
      <v-flex xs12 sm6 class="text-xs-center text-sm-left">
        <v-btn large router to="/meetup/new" class="secondary radius"> Create profile</v-btn>
      </v-flex> -->
      <!-- <v-flex xs12 sm6 offset-sm3 text-uppercase class="portal">Welcome to our registration portal</v-flex>
    </v-layout>
    <br>
    <br>
    <br>
    <v-layout>
          <v-flex xs12 sm6 offset-sm3 text-uppercase >fill in your course in the dropdown below</v-flex>
    </v-layout>
    <v-layout>
       
         <v-flex xs12 sm6 offset-sm3>
           <form>
             <v-layout>
             <v-select 
             label="Course"
             :selected="selected"
             :items="items" 
             v-model="selected"></v-select></v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-btn
                class="primary"
                
                @click.prevent="submitCourse()"
                type="submit">SUBMIT</v-btn>
            </v-flex>
          </v-layout>
         </form>
            </v-flex> -->
           
      <!-- <v-flex xs12 class="text-xs-center">
        <v-progress-circular
          indeterminate
          class="primary--text"
          :width="7"
          :size="70"
          v-if="loading"></v-progress-circular>
      </v-flex>
    </v-layout>
    <v-layout row wrap class="mt-2" v-if="!loading">
      <v-flex xs12>
        <v-carousel style="cursor: pointer;">
          <v-carousel-item
            v-for="meetup in meetups"
            :src="meetup.imageUrl"
            :key="meetup.id"
            @click="onLoadMeetup(meetup.id)">
            <div class="title">
              {{ meetup.title }}
            </div>
          </v-carousel-item>
        </v-carousel>
      </v-flex>
    </v-layout>
    <v-layout row wrap  class="mt-2">
      <v-flex xs12 class="text-xs-center">
       <p class="bolder2">Join our awesome Events!</p>
      </v-flex> -->
 
    
  </v-container>
</template>

<script>
  export default {
    
      data() {
        return{
        
      items: ['BSc. in Physics', 
      'BSc. in Analytical Chemistry', 
      'BSc. in Industrial Chemistry', 
      'BSc. in Biogeochemistry',
      'Bachelor of Science in Biochemistry',
      'BSc. in Statistics',
      'Bachelor of Science (BSc.)',
      'BSc. in Biology',
      'BSc. in Microbiology and Biotechnology',
      'BSc. in Environmental Conservation and Natural Resource',
      'BSc. in Environmental Sciences',
      'BSc. in Information Technology',
      'Diploma in information Technology',
      'Certificate in Computer & Portable Devices',
      'Certificate in Computer Repair & Maintenance',
      'Certificate in Computer Applications',
      'PhD in Physics',
      'Master of Science in Applied Parasitology',
      'Master of Science in Biology of Conservation',
      'Doctor of Philosophy in Applied Parasitology',
      'Doctor of Philosophy in Biology of Conservation',
      'Doctor of Philosophy in Applied Microbiology',
],
selected: ''
        }
      },
    computed: {
      meetups () {
        return this.$store.getters.featuredMeetups
      },
      loading () {
        return this.$store.getters.loading
      }
    },
    methods: {
      optionChanged:function (value) {
        this.$emit('update:option',value)
      },
      onLoadMeetup (id) {
        this.$router.push('/meetups/' + id)
      },
       submitCourse () {
         this.$emit("submitCourse")
      this.$router.push('/meetup/new')
      },
    }
  }
</script>

<style scoped>
.container {
  max-width: unset !important;
}
.Home{
 padding :0;
 max-width: 100vh;
}
.header {
  height: 91.2vh;
  position: relative;
  background-image:
   linear-gradient(to right, rgba(126, 213, 111, 0.801), rgba(40, 180, 133, 0.801)), url(../assets/home4.jpg);
  background-size: cover;
  padding:0;
}
.header__text-box{
   position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}
.heading-primary--main{
color: white;
font-family: "lato",sans-serif;
font-size: 3rem;
font-weight: 400;
} 
 .title {
   position: static;
   text-align: center;
   bottom: 50px;
   background-color: rgb(75, 49, 123, 0.8);
   color: white;
   box-sizing: border-box;
   font-size: 2em;
   padding: 10px;
}
.portal{
  font-family: 'Times New Roman', Times, serif;
  font-size: 25px;
  font-weight: bolder;
}

.radius {
    border-radius: 100px;
    margin-bottom: 30px;

    
    animation-name: moveInTop;
    animation-duration: 5s;
    animation-fill-mode: backwards; 
    animation-play-state: running;
    animation-timing-function: ease-out;
}



@keyframes moveInTop {
    0% {
     opacity: 0;
     transform: translateY(-30px);
    }

     100% {
     opacity: 1;
     transform: translate(0);
    }
}

.position {
    margin-right: 300px !important;
    margin-left: 300px!important;
}

.bolder2 {
    font-size: 30px;
    font-weight: bolder;
   

    animation-name: moveInBottom;
    animation-duration: 5s;
    animation-fill-mode: backwards; 
    animation-play-state: running;
    animation-timing-function: ease-out
}



@keyframes moveInBottom {
    0% {
     opacity: 0;
     transform: translateY(30px);
    }

     100% {
     opacity: 1;
     transform: translate(0);
    }
}
</style>
