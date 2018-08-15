<template>
  <div class="">
    <div class="single-goal" v-for="(item, idx) in sortGoalProps(goalProps, getCurrentDay)" v-bind:key="idx">
      <div class="row ">
        <div class="col-md-6 col-sm-12 single-goal-left">
          <div class="map-iframe">
            <iframe
              width="400"
              height="200"
              frameborder="0" style="border:0"
              v-bind:src="item.mapUrl()" allowfullscreen>
            </iframe>
          </div>

        </div>
        <div class="col-md-6 col-sm-12 single-goal-right">
          <span class="goal-title">{{ item.goal }}</span> <br />

          <div class="" v-if="item.lastCompleted === getCurrentDay()">
            <button class="btn-success" disabled>Goal Completed Today</button>
          </div>

          <div class="" v-else-if="currentUserLocationProps.latitude === '---' || currentUserLocationProps.longitude === '---'">
            <button class="btn-secondary" disabled><img class="loading-icon" src="https://loading.io/spinners/balls/lg.circle-slack-loading-icon.gif">Loading Data...</button>
          </div>

          <div class="" v-else-if="isTodayAGoalDay(item.when.day, getCurrentDay())">
            <button v-on:click="compareLocationFunc([item.latitude, item.longitude], item, getCurrentDay())" class="btn-primary">Complete Goal</button>
          </div>

          <div class="" v-else="">
            <button class="btn-secondary" disabled>Not a Goal Day</button>
          </div>

          <hr />
          <div class="row days-row justify-content-center">
            <div class="col-md-2" v-for="(day, idx2) in item.when.day" v-bind:key="idx2">
              <div class="day">
                {{ day.day }}
                {{ day.time }}
              </div>
            </div>
          </div>
        </div>
      </div>



    </div>
  </div>
</template>

<script>
export default {
  name: 'Goals',
  props: ['goalProps', 'currentUserLocationProps', 'compareLocationFunc'],
  data(){
    return {
      removeMapSquare: () => {
        let mapSquares = document.getElementsByAttribute('jstcache')
        for (let i = 0; i < mapSquares.length; i++) {
          mapSquares[i].remove()
        }
      },
      sortGoalProps: (goalProps, getCurrentDayFunc) => {
        let sortedArray = []
        let addedToArray = false
        for (let i = 0; i < goalProps.length; i++) {
          addedToArray = false
          console.log('goal props at i', goalProps[i])
          for(let j = 0; j < goalProps[i].when.day.length; j++) {
            console.log('goal props days', goalProps[i].when.day[j].day)
            if (goalProps[i].when.day[j].day === getCurrentDayFunc()) {
              console.log('hey', goalProps[i].when.day[j].day)
              sortedArray.unshift(goalProps[i])
              addedToArray = true
            }
          }
          if (!addedToArray) {
            sortedArray.push(goalProps[i])
          }
        }
        console.log('ran function')
        return sortedArray
      },
      getCurrentDay: () => {
        let theWeek = ['Sun', 'Mon', 'Tue', 'Wed', 'Thurs', 'Fri', 'Sat']
        var theDate = new Date();
        var theDay = theDate.getDay();

        return theWeek[theDay]
      },
      isTodayAGoalDay: (daysArray, getCurrentDay) => {
        let isGoalDay = false
        let dayStr = ''

        for (let i = 0; i < daysArray.length; i++) {
          dayStr += daysArray[i].day
        }

          if (dayStr.includes(getCurrentDay)) {
            isGoalDay = true
          }
        return isGoalDay
      },

    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  hr {
    max-width: 75%
  }
  .single-goal {
    margin:30px 0;
    border-top:none;
    border-radius:5px;
    font-size:36px;
    padding:25px 0;
    color:gray;
    background-color:white;
  },
  .day {
    font-size: 18px;
    color: silver;
    font-family: Varela Round;
    text-align: center;
  }
  .days-row {
    margin:0 auto;
  }
  button {
    border-radius: 5px;
    min-width:15vw;
    font-family: Baloo;
  }
  .loading-icon {
    max-width: 25px;
    margin-right:10px;
  }
  .goal-title {
    font-size: 36px;
    font-family: Baloo
  }
  /* .single-goal-left {
    padding-left:10vw
  }
  .single-goal-right {
    padding-right:10vw
  } */
  .map-iframe {
    border-radius:50%;
    max-width: 100%
  }
  .col-md-2 {
    text-align: center;
  }

</style>
