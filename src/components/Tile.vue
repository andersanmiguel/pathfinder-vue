<template>
  <div :class="['tile', {'hint': tile.hint, played: tile.played, error: tile.error}]" v-on:click="setActive"></div>
</template>
<script>
export default {
  props: ['tile'],
  methods: {
    setActive: function() {
      if (this.tile.played) {
        return;
      }
      this.$emit('clicked', this.tile.key);
    }
  }
}
</script>
