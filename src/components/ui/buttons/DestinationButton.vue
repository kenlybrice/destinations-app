<template>
  <div class="destination-button-wrapper">
    <component
      :is="dynamicActionIconComp"
      @click.native="$emit('update-favorite', {
        id: item.id,
        type: !item.isFavorite ? 'add' : 'remove',
      })"
    />
    <button
      class="button button--destination"
      :class="{
        'button--favorite': item.isFavorite,
      }"
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
import IconMinus from '@/components/ui/icons/IconMinus';

export default {
  name: 'DestinationButton',
  
  components: {
    IconLocation,
    IconPlus,
    IconMinus,
  },
  
  props: {
    item: VueTypes.object.def(() => {}),
  },
  
  computed: {
    dynamicActionIconComp() {
      return this.item.isFavorite ? 'IconMinus' : 'IconPlus';
    },
  },
};
</script>
