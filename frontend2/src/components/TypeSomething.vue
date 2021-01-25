<template>
  <div class="container w-75">
    <div class="row">
      <div class ="col">
      <p>{{text}}</p>
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
        autofocus
        rows="1"
        />
        <h1>{{writtenText}}</h1>
      </div>
    </div>
  </div>
</template>




<script>

export default {
  name: 'TypeSomething',
  props: {
    text: String,
    typeField: String,
    writtenText: Number,
  },
  methods:{ 
    onSpace() {
      let s = this.text.substring(this.writtenText, this.writtenText + this.typeField.length);
      if(this.typeField == s){
        this.writtenText += this.typeField.length
        this.typeField = "";
        
      }
    },
    onChange(){
    },
  }
}
</script>


<style scoped>
p {
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

