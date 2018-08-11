<template>
  <div class="">
    <div class="single-goal" v-for="(item, idx) in goalProps">
      {{ item.goal }} <br />
      <div class="" v-if="isTodayAGoalDay(item.when.day, getCurrentDay())">
        <button v-on:click="$emit('testingEmit', 'Blehh')" class="btn-primary">Complete Goal</button>
      </div>
      <div class="" v-else="">
        <button class="btn-secondary" disabled>Complete Goal</button>
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
  props: ['goalProps'],
  data(){
    return {
      getCurrentDay: () => {
        let theWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']

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
      testingEmit: () => {
        return 'Blah'
      }
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
