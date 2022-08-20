<template>
  <div id="app">
    <header>
      <h1>Win een fles</h1>
    </header>

    <Board ref="board" v-show="playing" @restart="restart" />
    <OptionsPane ref="optionsPane" @gameStart="start" v-show="!playing" />

  </div>
</template>

<script>
import Board from './components/Board'
import OptionsPane from './components/OptionsPane'

export default {
  name: 'app',
  components: {
    Board,
    OptionsPane
  },
  mounted: function () {
    this.start([{'image': '/static/img/bruc-m.8b7188a.jpeg', 'width': 400, 'height': 400, 'size': {'horizontal': 4, 'vertical': 4}}])
  },
  data () {
    return {
      playing: false
    }
  },

  methods: {
    start (...args) {
      console.log(...args)
      this.playing = true
      this.$refs.board.start(...args)
    },

    restart () {
      this.playing = false
      this.$refs.optionsPane.reset()
    }
  }
}
</script>

<style lang="scss">
*, *::before, *::after {
  box-sizing: border-box;
}

a {
  text-decoration: none;
  color: #368ba0;
}

#app {
  font: 14px/20px sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

  header {
    h1 {
      font-weight: 100;
      height: 80px;
      line-height: 80px;
      font-size: 38px;
    }
  }

  footer {
    color: #555;
    margin-top: 60px;
  }
}
</style>
