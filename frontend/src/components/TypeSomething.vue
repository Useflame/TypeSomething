<template >
<div class="container w-75" v-show="play">
  <div class="row">
    <div class ="col">
      <div class="type-field">
        <span style="color: green;">{{ greenText }}</span>
        <span style="text-decoration: underline;"> {{ text.substring(greenText.length).split(' ')[0] }}</span>
        <span v-for="word in text.substring(greenText.length).split(' ').slice(1)" :key="word">{{ word }}</span>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col">
      <input
      @keyup.space="onSpace"
      v-model="typeField"
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
    text: String,
  },
  data: () => ({
    greenText: '',
    word: '',
    timer: '',
    bg: {
      color: 'grey',
      backgroundColor: ''
    },
  }),
  methods:{ 
    onSpace() {
      let s = this.text.substring(this.greenText.length, this.greenText.length + this.typeField.length);
      if(this.typeField.trim() == s.trim()){
        this.greenText += this.typeField
        this.typeField = "";
      };
      if(this.text.trim() == this.greenText.trim()) {
        this.play = false;
      };
    },
    onChange(){
      let s = this.text.substring(this.greenText.length, this.greenText.length + this.typeField.length);
      if((this.typeField.trim() != s.trim())){
        this.bg.backgroundColor = 'red'
        this.bg.color='black'
      } else {
        this.bg.backgroundColor = ''
        this.bg.color = 'grey'
      }
    },
    getTime() {
      let end = new Date()
      return this.time - end
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

