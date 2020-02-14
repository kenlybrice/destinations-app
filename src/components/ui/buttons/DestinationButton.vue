<template>
  <div class="destination-button-wrapper">
    <IconPlus />
    <button
      class="button button--destination"
      @click="$emit('show-active-list-index-detail', item.index)"
    > 
      <span>
        <IconLocation />
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
  </div>
</template>

<script>
import VueTypes from 'vue-types';

import IconLocation from '@/components/ui/icons/IconLocation';
import IconPlus from '@/components/ui/icons/IconPlus';

export default {
  name: 'DestinationButton',
  
  components: {
    IconLocation,
    IconPlus,
  },
  
  props: {
    item: VueTypes.object.def(() => {}),
  },
};
</script>
