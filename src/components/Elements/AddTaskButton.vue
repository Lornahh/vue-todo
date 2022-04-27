<template>
  <button
    class="headerButton"
    :style="{ background: color }"
    @click="$emit('add-task')"
  >
    {{ text }}
  </button>
</template>

<script>
// Above, remember that the colon before style is just shorthand for v-bind. What
// it does is dynamically bind the style property (hence the style) set to the prop
// that is passed down, with a default of black as set below Also, the at symbol
// click is short hand for v-on, in this case used for click. Extra Side Note, this
// component is entirely reusable, if multiple buttons were added in the parent
// component they would scale dynamically.

export default {
  //Always name components as PascalCase
  name: "AddTaskButton",
  props: {
    text: {
      type: String,
      default: "Add Task",
    },
    color: {
      type: String,
      default: "black",
    },
  },
};
</script>

<style scoped></style>
