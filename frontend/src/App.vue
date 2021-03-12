<template>
  <div id="app">
    <Navbar />
    <Start v-show="playStatus === 'start'" :start="start($event)" />
    <TypeSomething
      v-show="playStatus === 'playing'"
      :end="end($event)"
      ref="input"
      :play="playStatus"
      :givenText="text"
    />
    <Result v-show="playStatus === 'result'" />
  </div>
</template>

<script>
import TypeSomething from "@/components/TypeSomething";
import Navbar from "@/components/Navbar";
import Result from "@/components/Result";
import Start from "@/components/Start";

export default {
  name: "App",
  components: {
    TypeSomething,
    Result,
    Start,
    Navbar,
  },
  data: () => ({
    playStatus: "start",
    text:
      "Text messaging, or texting, is the act of composing and sending electronic messages, typically consisting of alphabetic and numeric characters, between two or more users of mobile devices, desktops/laptops, or other type of compatible computer. Text messages may be sent over a cellular network, or may also be sent via an Internet connection.",
    startTime: undefined,
    endTime: undefined,
    result: {
      time: 0,
      wpm: 0,
    },
  }),
  methods: {
    end(newVal) {
      this.playStatus = newVal;
      this.endv = new Date().getTime();
      this.result.time = Math.round((this.endTime - this.startTime) / 1000);
      this.result.wpm = Math.round(
        (Math.round(this.text.length / 5) / this.result.time) * 60
      );
    },
    start(newVal) {
      this.start = new Date().getTime();
      this.endTime = newVal;
    },
  },
};
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
