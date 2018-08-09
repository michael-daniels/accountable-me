<template>
  <div class="">
    <div class="single-goal" v-for="(item, idx) in goals">
      {{ item.goal }} <br />
      <div class="" v-if="isTodayAGoalDay(item.when.day, getCurrentDay())">
        <button class="btn-primary">Complete Goal</button>
      </div>
      <div class="" v-else="">
        <button class="btn-secondary" disabled>No Goal for Today</button>
      </div>

      <hr />
      <div class="row days-row justify-content-center">
        <div class="col-md-2" v-for="day in item.when.day">
          <div class="day">
            {{ day.day }}
            <br />
            {{ day.time }}
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'Goals',
  data(){
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
            latitude:'blah',
            longitude:'blahblah'
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
      getCurrentDay: () => {
        let theWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']

        var theDate = new Date();
        var theDay = theDate.getDay();

        return theWeek[theDay]
      },
      isTodayAGoalDay: (daysArray, getCurrentDay) => {
        console.log('Days Array', daysArray)
        let isGoalDay = false
        let dayStr = ''

        for (let i = 0; i < daysArray.length; i++) {
          dayStr += daysArray[i].day
        }


        console.log('DAY STRING', dayStr)
          if (dayStr.includes(getCurrentDay)) {
            isGoalDay = true
            console.log(isGoalDay)
          }
        return isGoalDay
      }
    }
  },
  props: {

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
    font-family:Baloo;
    padding:25px 0;
    color:gray;
    background-color:white;
  },
  .day {
    font-size: 18px;
    color: silver;
  }
  .days-row {
    margin:0 auto;
  }
  button {
    border-radius: 5px;
    min-width:15vw;
  }

</style>
