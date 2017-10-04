<template>
  <div id="app">
    <div class="timer" v-if="timer > 0">{{ timer }}</div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      timer: 5,
      count: ''
    };
  },
  watch: {
    timer: function() {
      if (this.timer === 0) {
        clearInterval(this.count);
      }
    }
  },
  mounted: function() {
    this.countDown();
  },
  methods: {
    countDown: function() {
      this.count = setInterval(() => {
        this.timer--;
      }, 1000);
    }
  }
}
</script>
