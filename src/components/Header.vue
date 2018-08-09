<template>
  <div class="">
    <header class="row nav">
      <div class="logo col-6">
        accountable.me
      </div>
      <div class="current-user col-6">
        Hello, {{ current_user }}
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data(){
    return {
      current_user:'Michael'
    }
  },
  props: {
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Baloo');

  .nav {
    min-height: 40px;
    background-color: blue;
    padding:25px 50px;
    color:white;
    font-family: Baloo;
    border-radius: 5px;
  }
  .logo {
    display:inline-block;
    text-align:left;
    font-size:24px
  }
  .current-user {
    display:inline-block;
    text-align: right;
    margin-top:4px

  }
  header {
    max-width:100%;
    margin:0 auto;
  }
</style>
