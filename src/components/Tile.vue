<template>
  <div :class="['tile', {hint: tile.hint, played: tile.played, error: tile.error}]" v-on:click="setActive"> {{ tile.key }} </div>
</template>
<script>
export default {
  props: ['tile'],
  methods: {
    setActive: function() {
      this.$emit('clicked', this.tile.key);
    }
  }
}
</script>
