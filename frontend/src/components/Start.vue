<template>
  <div>
    <button
      class="btn btn-dark vertical-center"
      v-hotkey="keymap"
      @click="start"
      type="button"
    >
      Start
    </button>
  </div>
</template>

<script>
export default {
  name: "Start",
  props: [],
  computed: {
    keymap() {
      return {
        enter: this.start,
      };
    },
  },

  data: () => ({}),
  methods: {
    start() {
      this.$emit("start", "playing");
    },
  },
};
</script>

<style></style>
