<template>
<div>
  <button
    class="btn btn-dark"
    v-hotkey="keymap"
    v-show="playStatus === 'start'"
    @click="startf"
    type="button"
  >
  Start
  </button>
</div>
</template>

<script>
export default {
  name: 'Result',
  props: [],
  data: () => ({}),
  methods: {}
}
</script>

<style>
</style>