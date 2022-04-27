<template>
  <button
    class="headerButton"
    :style="{ background: color }"
    @click="$emit('delete-all-tasks')"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  //Always name components as PascalCase
  name: "DeleteAllTasksButton",
  props: {
    text: {
      type: String,
      default: "Delete All Tasks",
    },
    color: {
      type: String,
      default: "red",
    },
  },
};
</script>

<style scoped></style>
