<template>
  <div id="app">
    <TypeSomething :text="text" :greenText="greenText" :word="word" :bg="bg"/>
  </div>
</template>

<script>
import TypeSomething from './components/TypeSomething.vue'

export default {
  name: 'App',
  components: {
    TypeSomething
  },
  data() {
    return {
      text: 'The responses to the pandemic have resulted in global social and economic disruption, including the largest global recession since the Great Depression. It has led to the postponement or cancellation of events, widespread supply shortages exacerbated by panic buying, agricultural disruption and food shortages, and decreased emissions of pollutants and greenhouse gases. Many educational institutions have been partially or fully closed. Misinformation has circulated through social media and mass media. There have been incidents of xenophobia and discrimination against Chinese people and against those perceived as being Chinese or as being from areas with high infection rates.',
      greenText: '',
      word: '',
      bg: {
        color: 'grey',
        backgroundColor: ''
      }
    };

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
  margin-top: 60px;
}
</style>
