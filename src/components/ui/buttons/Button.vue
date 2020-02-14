<template>
  <button
    class="button">
    {{ text }}
  </button>
</template>

<script>
// Utility
import VueTypes from 'vue-types';

export default {
  name: 'Button',
  
  props: {
    text: VueTypes.string.def('Button'),
  },
};
</script>
