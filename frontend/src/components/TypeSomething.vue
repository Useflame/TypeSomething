<template>
<div class="container w-75">
  <div class="row">
    <div class ="col">
      <div class="type-field">
        <span class="right">{{ typedText }}</span>
        <span class="current-word right">{{ currentWord.substr(0, greenWord) }}</span>
        <span class="current-word wrong">{{ currentWord.substr(greenWord, redWord) }}</span>
        <span class="current-word">{{ currentWord.substr(greenWord + redWord)}}</span>
        <span class="wrong">{{ ' ' + text.substr(0, redWord - currentWord.length)}}</span>
        <span
          v-if="currentWord.length > redWord"
          >{{ ' ' + text }}</span>
        <span v-else>{{ text.substr(redWord - currentWord.length) }}</span>
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
      ref="typingField"
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
    play: String,
    givenText: String,
  },
  computed: {
    text: function() {
      return this.givenText.split(' ').slice(this.pointer + 1).join(' ')
    },
    currentWord: function() {
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
      if (this.typingField.trim() === this.currentWord) {
        this.typedText += this.currentWord + ' ';
        this.pointer++;
        this.typingField = '';
        this.greenWord = 0;
      }
      if (this.typedText.trim() === this.givenText) {
        this.typingField = '';
        this.endGame();
      }
    },
    onChange() {
      // When changing input field this function check whether it right or wrong.If right it highliting current word with green color. If wrong it changes text after typed corretly to red(on length of text in input field) from black to red background color of input to red. 
      if (this.isInputCorrect()) {
        this.makeInputRight();
      } else {
        this.makeInputWrong();
      }
    },
    endGame() {
      this.$emit('endGame', 'end')
    },
    isInputCorrect() {
      // Check if input field equal current word.
      return (this.currentWord.indexOf(this.typingField.trim()) != -1)
    },
    /*
    Clear background color of input.
    Change variables which helps highliting text.
    */
    makeInputRight() {
      this.bg.backgroundColor = '';
      this.bg.color = 'grey';
      this.redWord = 0;
      this.greenWord = this.typingField.length;
    },
    /*
    Change styling of input.
    Change color of worng text to red.
    */
    makeInputWrong() {
      this.bg.backgroundColor = 'red';
      this.bg.color='black';
      this.redWord = this.typingField.length - this.greenWord;
    },
  }
}
</script>


<style scoped>
.right {
  color: green;
}
.wrong {
  color: red;
}
.current-word {
  text-decoration: underline;
}
.type-field {
  font-size: 1.1em;
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

