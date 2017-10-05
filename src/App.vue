<template>
  <div id="app">
    <timer :initial="initial_timer" v-on:count_end="end_count"></timer>
    <p>Ended: {{ count_ended }}</p>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      initial_timer: 5,
      count_ended: 'nope'
    };
  },
  watch: {
  },
  mounted: function() {
  },
  methods: {
    end_count: function() {
      this.count_ended = 'yep';
    }
  }
}
</script>
