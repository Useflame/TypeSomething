<template>
  <div class="container w-75">
    <div class="row">
      <div class ="col">
      <p>Voting was not able to take place in many areas of the country controlled by armed groups resulting in some Central African media and opposition candidates describing the elections as farce and fraud.[4][5] Some 800 of the country's polling stations, 14% of the total, were closed due to violence,[6] and during the first round, voting was unable to take place in 29 of the 71 sub-prefectures, while six others only managed to partially vote before being shut down due to voter intimidation.[7]</p>
    </div>
    </div>
    <div class="row">
      <div class="col">
      <input
          spellcheck="false"
          autocomplete="off"
          v-model="message"
          class="w-100"
          autofocus
          rows="1"
          @keyup.space="warning"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options({
  props: {
    msg: String
  }
})
export default class TypeSomething extends Vue {
  msg!: string
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
</style>
