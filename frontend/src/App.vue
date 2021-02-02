<template>
  <div
    id="app"
    @keyup.enter="play=play"
  >
    <Header />
    <button
      class="btn btn-light vertical-center"
      @keyup.enter="play=true"
      @click="play=true"
      ref="type-field"
      v-show="!play"
      type="button"
      autofocus
    >
    Start
    </button>
    <TypeSomething
      :givenText="text"
      v-on:endGame="end($event)"
      v-show="play"
      :play="play"
    />
  </div>
</template>

<script>
import TypeSomething from '@/components/TypeSomething'
import Header from '@/components/Header'

export default {
  name: 'App',
  components: {
    TypeSomething,
    Header
  },
  data: () => ({
      play: false,
      text: 'A wiki is a hypertext publication collaboratively edited and managed by its own audience directly using a web browser. A typical wiki contains multiple pages for the subjects or scope of the project and could be either open to the public or limited to use within an organization for maintaining its internal knowledge base.'
  }),
  methods: {
    end(newVal) {
      this.play = newVal;
    }
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