<template>
  <form id="optionsForm" @submit.prevent="start">
    <img :src="image" v-if="image" with="400" height="400">
    <div>
      <div>
        <label for="file">
          Select an image
          <input type="file"
            id="file"
            accept="image/gif, image/jpeg, image/png"
            @change="fileChanged">
        </label>
        Board size:
        <input type="number" name="width" min="2" max="10" v-model.number="size.horizontal">
        ×
        <input type="number" name="height" min="2" max="10" v-model.number="size.vertical">
      </div>
      <button v-if="image">Start</button>
    </div>
  </form>
</template>

<script>
import loadImage from 'blueimp-load-image'
import board from '../assets/bruc-m.jpeg'

export default {
  data () {
    return {
      image: board,
      size: {
        horizontal: 4,
        vertical: 4
      }
    }
  },

  methods: {
    fileChanged (e) {
      if (!e.target.files.length) {
        this.image = null
        return
      }

      loadImage(board, canvas => {
        this.image = canvas.toDataURL()
      }, {
        maxWidth: 600,
        maxHeight: 600,
        minWidth: 200,
        minHeight: 200,
        canvas: true
      })
    },

    /**
     * Start the game by emitting the event.
     */
    start () {
      this.$emit('gameStart', {
        image: this.image,
        size: this.size,
        width: 600,
        height: 600
      })
    },

    /**
     * Reset the options.
     */
    reset () {
      this.image = null
      document.querySelector('#optionsForm').reset()
    }
  }
}
</script>

<style lang="scss" scoped>
img {
  border: 1px solid #ccc;
  margin-bottom: 8px;
}

label[for=file] {
  color: #368ba0;
  cursor: pointer;
  display: inline-block;
  margin-right: 12px;
}

input[type=number] {
  height: 24px;
  font-size: 14px;
  border: 1px solid #ccc;
}

input[type=file] {
  display: none;
}

button {
  -webkit-appearance: none;
  padding: 6px 12px;
  background: #1ca76a;
  color: #fff;
  border-radius: 3px;
  border: 0;
  font-size: 14px;
  cursor: pointer;
  margin-top: 10px;
}
</style>
