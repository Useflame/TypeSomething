<template>
  <div
    id="app"
    @keyup.enter="play=true"
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
      :text="text"
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
      text: 'The responses',
  })
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