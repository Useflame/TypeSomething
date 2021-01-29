<template>
  <div class="container w-75">
    <div class="row">
      <div class ="col">
      
        <div class="type-field">
          <span class="right">{{ text.substring(0, writtenText.length) }}</span>
          <span class="wrong"></span>
          <span style="text-decoration: underline">
          {{ text.substring(writtenText.length).split(' ').slice(0, 1)[0]}}
          </span>
          <span v-for="word in text.substring(writtenText.length).split(' ').slice(1)" :key ="word">{{ word + ' ' }}</span>
        </div>
    </div>
    </div>
    <div class="row">
      <div class="col">
      <input

        v-model="typeField"
        autocomplete="off"
        spellcheck="false"
        @keyup="onSpace"
        class="w-100"
        autofocus
        rows="1"
        />
      </div>
    </div>
  </div>
</template>




<script>
import Vue from 'vue';
import TextHighlight from 'vue-text-highlight';

Vue.component('text-highlight', TextHighlight);


export default {
  name: 'TypeSomething',
  props: {
    text: String,
    typeField: String,
    writtenText: String,
  },
  methods:{ 
    onSpace() {
      let s = this.text.substring(this.writtenText.length, this.writtenText.length + this.typeField.length);
      if(this.typeField == s){
        this.writtenText += this.typeField
        this.typeField = "";
      }
    },
    onChange(){
    },
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
}
.right {
  color: green;
}
.wrong {
  color: red;
}
</style>

