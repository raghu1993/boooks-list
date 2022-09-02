<template>
  <div class="" id="app">
    <div class="left">
      <img width="150" src="./assets/bmuse_logo.png" alt="logo">
    </div>
    <div class="right searchDiv ">
      <img src="./assets/search.png" alt="search">
    </div>

    <div>
      <h1 style="visibility : hidden">.</h1>
    </div>
    <bg-compo></bg-compo>
    <book-list></book-list>
  </div>

</template>


<script>
import BgCompo from "./components/bg.vue";
import bookList from "./components/bookList.vue";
export default {
  name: 'App',
  components: {
    'bg-compo' :  BgCompo,
    'book-list': bookList,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  margin-left: 40px;
  margin-right: 40px;
}

body {
  background-image: url('./assets/bg.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}

.left {
  float: left;
}

.right {
  float: right;
}

.searchDiv{
  height: 15px;
    width: 15px;
    border: 10px solid #1f2021bf;
    border-radius: 20px;
}
</style>
