<template>
  <div class="timer" v-if="timer > 0">{{ timer }}</div>
</template>

<script>
export default {
  props: ['initial'],
  data: function() {
    return {
      timer: this.initial,
      count: ''
    };
  },
  watch: {
    timer: function() {
      if (this.timer === 0) {
        clearInterval(this.count);
        this.$emit('count_end');
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

