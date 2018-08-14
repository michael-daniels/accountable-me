<template>
  <div id="app">
    {{getLocation(updateUserLocation)}}
    <Header />
    <!-- <span>LATITUDE: </span><div v-text="currentUserLocation.latitude"></div>
    <span>LONGITUDE: </span><div v-text="currentUserLocation.longitude"></div>
    <button v-on:click="isAtGoalLocation(testingLocationData)">Check Current Location Against Sample Location</button> -->
    <Goals v-bind:goalProps="goals" v-bind:currentUserLocationProps="currentUserLocation" v-bind:compareLocationFunc="isAtGoalLocation"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Goals from './components/Goals.vue'
import 'bootstrap/dist/css/bootstrap.min.css';

export default {
  name: 'app',
  components: {
    Goals,
    Header
  },
  data() {
    return {
      goals: [
        {
          goal:'Home',
          lastCompleted:'',
          when: {
            day:[
              {
                day:'Monday',
                time:'6:00pm'
              },
              {
                day:'Tuesday',
                time:'6:00pm'
              },
              {
                day:'Wednesday',
                time:'6:00pm'
              },
              {
                day:'Thursday',
                time:'6:00pm'
              },
              {
                day:'Friday',
                time:'6:00pm'
              }
            ],
          },
          latitude: 33.428410,
          longitude: -112.233007,
          mapUrl: function() {
            return `https://www.google.com/maps/embed/v1/view?key=AIzaSyComtCTHcgK-Hn-t4e_idADPWJgWpI4G4E&center=${this.latitude},${this.longitude}&zoom=17`
          }
        },
        {
          goal:'Go to the gym',
          lastCompleted:'',
          when: {
            day:[
              {
                day:'Monday',
                time:'6:00pm'
              },
              {
                day:'Wednesday',
                time:'6:00pm'
              },
              {
                day:'Friday',
                time:'6:00pm'
              }
            ],
          },
          latitude: 33.479278,
          longitude: -112.217833,
          mapUrl: function() {
            return `https://www.google.com/maps/embed/v1/view?key=AIzaSyComtCTHcgK-Hn-t4e_idADPWJgWpI4G4E&center=${this.latitude},${this.longitude}&zoom=17`
          }
        },
        {
          goal:'Go to co-working space',
          lastCompleted:'',
          when: {
            day:[
              {
                day:'Monday',
                time:'6:00pm'
              },
              {
                day:'Tuesday',
                time:'6:00pm'
              },
              {
                day:'Thursday',
                time:'6:00pm'
              },
              {
                day:'Friday',
                time:'6:00pm'
              }
            ],
            time: '6:00am',
          },
          latitude: 33.4397,
          longitude: -112.0672,
          mapUrl: function() {
            return `https://www.google.com/maps/embed/v1/view?key=AIzaSyComtCTHcgK-Hn-t4e_idADPWJgWpI4G4E&center=${this.latitude}, ${this.longitude}&zoom=17`
          }
        },
        {
          goal:'Take Sparky for a walk',
          lastCompleted:'',
          when: {
            day:[
              {
                day:'Monday',
                time:'6:00pm'
              },
              {
                day:'Tuesday',
                time:'6:00pm'
              },
              {
                day:'Thursday',
                time:'6:00pm'
              }
            ],
            time: '6:00am',
          },
          latitude: 33.428130,
          longitude: -112.230010,
          mapUrl: function() {
            return `https://www.google.com/maps/embed/v1/view?key=AIzaSyComtCTHcgK-Hn-t4e_idADPWJgWpI4G4E&center=${this.latitude}, ${this.longitude}&zoom=17`
          }
        },
      ],
      currentUserLocation: {
        latitude:'---',
        longitude:'---'
      },
      testingLocationData: [33.440400, -112.067077]
    }
  },
  methods: {
      updateUserLocation(latitude, longitude) {
        this.currentUserLocation.latitude = Number(latitude)
        this.currentUserLocation.longitude = Number(longitude)
        console.log(this.currentUserLocation)
      },
      getLocation(updateUserLocationFunc) {
        let latitude;
        let longitude;
        if (navigator.geolocation) {
          navigator.geolocation.getCurrentPosition(function (position) {
            latitude = position.coords.latitude.toFixed(4)
            longitude = position.coords.longitude.toFixed(4)
            updateUserLocationFunc(latitude, longitude)
            })
        } else {
          alert("Geolocation is not supported by this browser.")
        }
      },
      isAtGoalLocation(goal, item, currentDay) {
        if ((this.currentUserLocation.latitude > goal[0] - .0009 && this.currentUserLocation.latitude < goal[0] + .0009) && (this.currentUserLocation.longitude > goal[1] - .0009 && this.currentUserLocation.longitude < goal[1] + .0009)) {
          let goalClicked = item

          for (let i = 0; i < this.goals.length; i++) {
            if (this.goals[i].goal === item.goal) {
              this.goals[i].lastCompleted = currentDay
            }
          }
          console.log(this.goals)
          //alert('Location Match')
          return true
        } else {
          alert('Not Close Enough to Location')
          return false
        }
      }
  }
}

</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Varela+Round');
  body {
    background-color:#eeeeee;
    max-width:90%;
    margin:0 auto;
    text-align:center;
    padding:6vh;
  }
</style>
