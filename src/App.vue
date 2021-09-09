<template>
  <div id="app">
    <div class="logo">
      <img src="logo.svg" alt="">
      <h4>Feedbacky</h4>
    </div>
    <h2 class="title">Get User feedback instantly !</h2>
    <div class="container">
      <div class="board">
        <Search />
        <ListRequest />
      </div>
      <FormRequest />
    </div>
  </div>
</template>

<script>
import FormRequest from './components/FormRequest.vue'
import ListRequest from './components/ListRequest.vue'
import Search from './components/Search.vue'

export default {
  name: 'App',
  components: {
    FormRequest,
    ListRequest,
    Search
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;500;600&display=swap');

  *,
  *::after,
  *::before {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  #app {
    font-family: 'Rubik', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }
  .title {
    margin: 30px 0;
    font-size: 50px;
    font-weight: 500;
    text-align: center;
  }
  .container {
    max-width: 1170px;
    margin: 30px auto;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  .board {
      flex: 1;
      margin-right: 20px;
  }
  input, textarea {
     font-family: 'Rubik', sans-serif;
     font-size: 15px;
  }
  .logo {
    margin-top: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .logo img {
    font-size: 40px;
    width: 70px;
  }
  .logo h4 {
    display: inline-block;
    margin-left: 10px;
    font-size: 30px;
  }
</style>
