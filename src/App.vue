<template>
  <div id="app">
    <h1>PathFinder</h1>
    <p>The game, not the robot.</p>
    <!--<timer :initial="initial_timer" v-on:count_end="end_count"></timer>-->

    <div :class="'board tile'+grid">
      <tile :key="tile.key" :tile="tile" v-on:clicked="checkTile" v-for="tile in board"></tile>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      initial_timer: 5,
      level: 0,
      initial_grid: 3,
      board: []
    };
  },
  computed: {
    grid: function() {
      return this.level + this.initial_grid;
    }
  },
  watch: {
  },
  mounted: function() {
    this.make_board();
  },
  methods: {
    make_board: function() {
      let board = [];
      let tiles = this.grid * this.grid;
      for (let i = 1; i <= tiles; i++) {
        board.push({ key: i, hint: false, played: false, error: false});
      }
      this.board = board;
    },
    checkTile: function(tile_index) {
      console.log(tile_index);
    },
    end_count: function() {
      // Timer end
    }
  }
}
</script>


<style lang="scss" src="./assets/styles/main.scss"></style>
