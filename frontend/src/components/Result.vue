<template>
  <div>
    <div class="col">
      <p>Your time: {{ result.time }}</p>
      <p>Your wpm: {{ result.wpm }}</p>
    </div>
    <button
      class="btn btn-dark vertical-center col"
      v-hotkey="keymap"
      @click="startf"
      type="button"
    >
      Play again
    </button>
  </div>
</template>

<script>
export default {
  name: "Result",
  data: () => ({}),
  methods: {},
};
</script>

<style></style>
