<template>
  <div id="app">
    <h1 class="">{{ title }}</h1>
    <Destinations />
  </div>
</template>

<script>
import Destinations from "./components/Destinations";

export default {
  name: "App",

  components: {
    Destinations,
  },
  
  data() {
    return {
      title: 'Country Travel Information',
    };
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #f2f2f2;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
