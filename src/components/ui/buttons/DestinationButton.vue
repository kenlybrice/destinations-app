<template>
  <button
    class="button button--destination"
  > 
    <span>
      <svg xmlns="http://www.w3.org/2000/svg" id="icon-location" width="24" height="24" viewBox="0 0 24 24"><path d="M12 0c-4.198 0-8 3.403-8 7.602 0 4.198 3.469 9.21 8 16.398 4.531-7.188 8-12.2 8-16.398 0-4.199-3.801-7.602-8-7.602zm0 11c-1.657 0-3-1.343-3-3s1.343-3 3-3 3 1.343 3 3-1.343 3-3 3z"/></svg>
      <span
        class="button__title"
        v-if="item.geopoliticalarea"
        v-html="item.geopoliticalarea"
      /><br>
      <span
        class="button__data"
        v-if="item.last_update_date"
        v-html="item.last_update_date"
      />
    </span>
  </button>
</template>

<script>
import VueTypes from 'vue-types';

export default {
  name: 'DestinationButton',
  
  props: {
    item: VueTypes.object.def(() => {}),
  },
};
</script>

<style>
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
  text-align: center;
  transition: all .3s ease-in-out;
  width: 32%;
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

#icon-location {
  opacity: .5;
  display: block;
  margin: 20px auto;
  transition: all .3s ease-in-out;
}

.button--destination:hover #icon-location {
  transform: translateY(-40%) scale(2);
}
</style>