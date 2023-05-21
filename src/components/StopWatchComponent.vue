<template>
  <h1>
    <strong>{{ elapsedTime }}</strong>
  </h1>
</template>

<script lang="ts">

import { defineComponent } from 'vue';

export default defineComponent({
  name: 'StopWatchComponent',
  props: {
    timeInSeconds: {
      type: Number,
      default: 0
    }
  },
  computed: {
    elapsedTime () : string {
      return new Date(this.timeInSeconds * 1000).toISOString().substr(11, 8);
    }
  },
});

</script>

<style scoped>

h1 {
  font-size: 3rem;
  font-weight: bold;
  color: #363636;
}

</style>