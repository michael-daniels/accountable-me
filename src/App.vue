<template>
  <div id="app">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.2.0/css/all.css" integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ" crossorigin="anonymous">
    {{getLocation(updateUserLocation)}}
    <Header />
    <button class="btn-primary add-goal-plus"><span class="plus-square"><i class="far fa-plus-square"></i><span> Add New Goal</span></span></button>
    <form class="add-goal-form" action="" method="">
      <input class="form-control" type="text" name="goalTitle" v-model:value="newGoal.goal" placeholder="Goal Title">
      <select class="form-control" name="" v-model:value="newGoal.days" multiple>
        <option value="Sun">Sunday</option>
        <option value="Mon">Monday</option>
        <option value="Tue">Tuesday</option>
        <option value="Wed">Wednesday</option>
        <option value="Thurs">Thursday</option>
        <option value="Fri">Friday</option>
        <option value="Sat">Saturday</option>
      </select>
      <input class="form-control" type="text" name="goalTime" v-model:value="newGoal.when.time" placeholder="Time">
      <input class="form-control" type="text" name="goalLatitude" v-model:value="newGoal.latitude" placeholder="Latitude">
      <input class="form-control" type="text" name="goalLongitude" v-model:value="newGoal.longitude" placeholder="Longitude">
      <button v-on:click="addNewGoal" class="btn-primary form-control add-goal-btn">Add a Goal</button>
    </form>
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
                day:'Mon',
                time:'6:00pm'
              },
              {
                day:'Tue',
                time:'6:00pm'
              },
              {
                day:'Wed',
                time:'6:00pm'
              },
              {
                day:'Thurs',
                time:'6:00pm'
              },
              {
                day:'Fri',
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
                day:'Mon',
                time:'6:00pm'
              },
              {
                day:'Wed',
                time:'6:00pm'
              },
              {
                day:'Fri',
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
                day:'Mon',
                time:'6:00pm'
              },
              {
                day:'Tue',
                time:'6:00pm'
              },
              {
                day:'Thurs',
                time:'6:00pm'
              },
              {
                day:'Fri',
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
                day:'Mon',
                time:'6:00pm'
              },
              {
                day:'Tue',
                time:'6:00pm'
              },
              {
                day:'Thurs',
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
      addGoalFormHidden: true,
      newGoal: {
        goal:'',
        lastCompleted:'',
        days:[],
        when: {
          day: [],
          time:''
        },
        latitude: null,
        longitude: null,
        mapUrl: function() {
          return `https://www.google.com/maps/embed/v1/view?key=AIzaSyComtCTHcgK-Hn-t4e_idADPWJgWpI4G4E&center=${this.latitude}, ${this.longitude}&zoom=17`
        }
      },
      testingLocationData: [33.440400, -112.067077]
    }
  },
  methods: {
      addNewGoal() {
        console.log('button clicked', this.newGoal.days)
        for (let i = 0; i < this.newGoal.days.length; i++) {
          this.newGoal.when.day.push({
            day:this.newGoal.days[i],
            time:this.newGoal.when.time
          })
        }
        this.newGoal.latitude = Number(this.newGoal.latitude)
        this.newGoal.longitude = Number(this.newGoal.longitude)
        this.goals.push(this.newGoal)
      },
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
  .add-goal-btn {
    margin-top:25px
  }
  .day-select {
    min-width: 100%
  }
  .add-goal-form {
    display:none;
  }
  .plus-square {
    font-size: 18px;
    font-family:Baloo
  }
  .add-goal-plus {
    margin-top: 25px;
    padding: 10px 25px;
    border-radius: 5px;
  }
</style>
