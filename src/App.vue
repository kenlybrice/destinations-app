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

/* BUTTON */
.button {
  font-size: 16px;
  margin: 0 20px;
  padding: 10px 20px;
}

/* DESTINATION */
.destination-button-wrapper {
  position: relative;
  text-align: center;
  transition: all .3s ease-in-out;
  width: 32%;
}

.destination-button-wrapper .icon-plus {
  position: absolute;
  top: 20px;
  right: 20px;
}

.destination-button-wrapper .icon-plus:hover {
  transform: scale(1.2);
  transition: all .2s ease-in-out;
}

.button--destination {
  align-items: center;
  background-color: #666;
  color: #FFFFFF;
  font-size: 18px;
  display: flex;
  height: 250px;
  justify-content: center;
  margin: 2px;
  padding: 20px;
  width: 100%;
}

.button--destination:hover {
  background-color: #FFFFFF;
  color: #333333;
}

.button--destination .button__title {
  font-size: 18;
  font-weight: bold;
}

.button--destination .button__data {
  font-size: 12px;
}

.button--destination:hover .icon-location {
  transform: translateY(-40%) scale(2);
}

/* ICON */
.icon-location {
  opacity: .5;
  display: block;
  margin: 20px auto;
  transition: all .3s ease-in-out;
}

/* SHADOW */
.shadow {
  -webkit-box-shadow: 10px 10px 53px 10px rgba(0,0,0,0.23);
  -moz-box-shadow: 10px 10px 53px 10px rgba(0,0,0,0.23);
  box-shadow: 10px 10px 53px 10px rgba(0,0,0,0.23);
}

/* DESTINATIONS */
.destination__list {
  display: flex;
  flex-wrap: wrap;
  height: ;
  max-width: 1024px;
  margin: 50px auto;
  width: 100%;
  transition: all .3s ease-in-out;
}

.destination__list-control {
  display: block;
}

.blur-effect {
  /* filter: blur(10px); */
  opacity: .4;
  transition: all .8s ease-in-out;
  transform: scale(.8);
}

.destination__details {
  background-color: #f2f2f2;
  border: solid 1px #666;
  margin: 0 auto;
  max-width: 800px;
  opacity: 0;
  padding: 40px;
  transition: all .3s ease-in-out;
}

.destination__details-content {
  overflow-y: scroll;
  text-align: left;
  height: 600px;
}

.destination__details.active {
  opacity: 1;
  transform: translateY(-770px);
  transition: all .3s ease-in-out;
}

</style>
