<template>
  <div id="app" >
    <Navbar />
    <span  /> 
    <button
      class="btn btn-dark vertical-center row"
      v-hotkey="keymap"
      v-show="playStatus === 'start'"
      @click="startf"
      type="button"
    >
    Start
    </button>
    <div v-show="playStatus=='end'" class="row">
      <div class="col">
        <p>Your time: {{ result.time }}</p>
        <p>Your wpm: {{ result.wpm }}</p> 
      </div>
      <button
        class="btn btn-dark vertical-center col"
        v-hotkey="keymap"
        @click="startf"
        type="button"
      >
      Play again
      </button>
    </div>


    <TypeSomething
      v-show="playStatus === 'playing'"
      v-on:endGame="end($event)"
      ref="input"
      :play="playStatus"
      :givenText="text"
    />

  </div>
</template>

<script>
import TypeSomething from '@/components/TypeSomething'
import Navbar from '@/components/Navbar'

export default {
  name: 'App',
  components: {
    TypeSomething,
    Navbar
  },
  computed: {
    keymap () {
      return {
        'enter': this.startf
      }
    }
  },
  data: () => ({
      playStatus: 'start',
      text: 'A wikiasldkjhf;lksdj a;lfkjdsa;lkfj ;lkdsjf ;lkadjs;lkdfjs .',
      start: undefined,
      endv: undefined,
      result: {
        time: 0,
        wpm: 0
      }
  }),
  methods: {
    end(newVal) {
      this.playStatus = newVal;
      this.endv = new Date().getTime();
      this.result.time = Math.round((this.endv - this.start) / 1000);
      this.result.wpm = Math.round(Math.round(this.text.length / 5) / this.result.time * 60);
    },
    startf() {
      this.start = new Date().getTime();
      this.playStatus = 'playing';
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.vertical-center {
  margin: 0;
  position: absolute;
  top: 50%;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
}
</style>