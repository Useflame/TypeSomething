<template>
<div class="container w-75">
  <div class="row">
    <div class ="col">
      <div class="type-field">
        <span style="color: green;">{{ typedText }}</span>
        <span style="text-decoration: underline; color:green;">{{ word.substr(0, greenWord) }}</span>
        <span style="text-decoration: underline; color: red">{{ word.substr(greenWord, redWord) }}</span>
        <span style="text-decoration: underline;">{{ word.substr(this.greenWord + this.redWord)}}</span>
        <span style="color: red;">{{ ' ' + text.substr(0, redWord - word.length)}}</span>
        <span v-if="word.length > redWord">{{ ' ' + text }}</span>
        <span v-else>{{ text.substr(redWord - word.length) }}</span>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col">
      <input
      @keyup.space="onSpace"
      v-model="typingField"
      autocomplete="off"
      spellcheck="false"
      @keyup="onChange"
      class="w-100"
      :style="bg"
      rows="1"
      />
    </div>
  </div>
</div>
</template>




<script>
export default {
  name: 'TypeSomething',
  props: {
    play: Boolean,
    givenText: String,
  },
  computed: {
    text: function() {
      return this.givenText.split(' ').slice(this.pointer + 1).join(' ')
    },
    word: function() {
      return this.givenText.split(' ')[this.pointer]
    }
  },
  data: () => ({
    greenWord: 0,
    redWord: 0,
    pointer: 0,
    typedText: '',
    typingField: '',
    bg: {
      color: 'grey',
      backgroundColor: ''
    }
  }),
  methods: {
    onSpace() {
      if(this.typingField.trim() === this.word){
        this.typedText += this.word + ' ';
        this.pointer++;
        this.typingField = '';
        this.greenWord = 0;
      }
      if(this.typedText.trim() === this.givenText) {
        this.endGame();
      }
    },
    onChange() {
      if(this.typingField.trim() == this.word.substr(0, this.typingField.length)){
        this.bg.backgroundColor = '';
        this.bg.color = 'grey';
        this.redWord = 0;
        this.greenWord = this.typingField.length;
      } else {
        this.redWord = this.typingField.length - this.greenWord;
        this.bg.backgroundColor = 'red';
        this.bg.color='black';
      }
    },
    endGame() {
      this.$emit('endGame', false)
    }
  }
  }
</script>


<style scoped>
.type-field {
  text-align: left;
  padding: 0;
  /*Turn off copying text*/
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -o-user-select: none;
  user-select: none;
  margin-top: 60px;
}
</style>

