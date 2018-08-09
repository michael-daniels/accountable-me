<template>
  <div id="app">
    <Header />
    <Goals />
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
      getLocation: () => {
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(showPosition);
            } else {
                alert("Geolocation is not supported by this browser.")
            }
        }
        getLocation()
        function showPosition(position) {
            console.log(position.coords.latitude)
            console.log(position.coords.longitude)
        }
      }
    }
  },
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
