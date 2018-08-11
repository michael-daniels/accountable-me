<template>
  <div id="app">
    {{getLocation(updateUserLocation)}}
    <Header />
    <span>LATITUDE: </span><div v-text="currentUserLocation.latitude"></div>
    <span>LONGITUDE: </span><div v-text="currentUserLocation.longitude"></div>
    <button v-on:click="isAtGoalLocation(testingLocationData)">Check Current Location Against Sample Location</button>
    <Goals v-bind:goalProps="goals"/>
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
          goal:'Go to the gym',
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
            latitude:'blah',
            longitude:'blahblah'
          }
        },
        {
          goal:'Go to co-working space',
          when: {
            day:[
              {
                day:'Monday',
                time:'6:00pm'
              },
              {
                day:'Thursday',
                time:'6:00pm'
              }
            ],
            time: '6:00am',
            latitude:'33.44037840000001',
            longitude:'-112.0671339'
          }
        },
        {
          goal:'Take Sparky for a walk',
          when: {
            day:[
              {
                day:'Monday',
                time:'6:00pm'
              },
              {
                day:'Thursday',
                time:'6:00pm'
              }
            ],
            time: '6:00am',
            latitude:'blah',
            longitude:'blahblah'
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
        this.currentUserLocation.latitude = latitude
        this.currentUserLocation.longitude = longitude
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
      isAtGoalLocation(goal) {
        if ((this.currentUserLocation.latitude > goal[0] - .0009 && this.currentUserLocation.latitude < goal[0] + .0009) && (this.currentUserLocation.longitude > goal[1] - .0009 && this.currentUserLocation.longitude < goal[1] + .0009)) {
          alert('Location Match')
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
  body {
    background-color:#eeeeee;
    max-width:90%;
    margin:0 auto;
    text-align:center;
    padding:6vh;
  }
</style>
