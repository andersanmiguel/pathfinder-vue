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
import game from './modules/game'
export default {
  data: function() {
    return {
      initial_timer: 5,
      level: 2,
      initial_grid: 3,
      level_values: [],
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
    this.prepareLevel();
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


    prepareLevel: function() {
      this.level_values = [];
      let row = this.grid;
      let current = game.getRandomInt(this.grid * this.grid - this.grid + 1, this.grid * this.grid);
      this.level_values.push(current);
      this.nextValid(current, row);
      this.paintHint();
    },

    paintHint: function() {
      this.level_values.forEach((item) => {
        this.board[item - 1].hint = true;
      });
    },

    nextValid: function(current, row) {
      let row_values = this.row_values(row);
      if (row === 1 && row_values.includes(current)) {
        return 1;
      } else {

        let posibilities = [];

        if (row_values.includes(current - 1)) {
          posibilities.push(current - 1);
        }

        if (row_values.includes(current + 1)) {
          posibilities.push(current + 1);
        }

        posibilities.push(current - this.grid);

        let filtered = posibilities.filter((item) => {
          return !this.level_values.includes(item);
        });

        let next_index = game.getRandomInt(0, filtered.length - 1);

        let next = filtered[next_index];

        this.level_values.push(next);

        if (!row_values.includes(next) && row > 1) {
          row--;
        }

        return this.nextValid(next, row);

      }
    },
    row_values: function(row) {
      let values = [];
      for (let i = 1; i <= this.grid; i++) {
        values.push(row * this.grid - i + 1);
      }
      return values;
    },
    end_count: function() {
      // Timer end
    }
  }
}
</script>


<style lang="scss" src="./assets/styles/main.scss"></style>
