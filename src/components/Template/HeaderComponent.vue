<template>
  <header>
    <div class="HeaderContainer">
      <h1 class="headerTitle">{{ title }}</h1>
      <DeleteAllTasksButton
        text="Delete All Tasks"
        color="Red"
        @delete-all-tasks="$emit('delete-all-tasks')"
      />
      <AddTaskButton
        text="Add Task"
        color="green"
        @add-task="$emit('add-task')"
      />
    </div>
  </header>
</template>

<script>
import AddTaskButton from "../Elements/AddTaskButton";
import DeleteAllTasksButton from "../Elements/DeleteAllTasksButton";
export default {
  //Always name component as PascalCase
  name: "HeaderComponent",
  props: {
    title: {
      //Almost like TypeScript here. Always keep type of prop in check.
      type: String,

      // Default is used if the prop is not passed (As in title='Task Tracker' in parent component call)
      default: "Task Tracker",
    },
  },

  //Always have to import child component!
  components: { AddTaskButton, DeleteAllTasksButton },
};
</script>

<style scoped>
.HeaderContainer {
  display: flex;
  justify-content: center;
  align-items: center;
}
header h1 {
  font-size: 3rem;
  margin-right: 1.5rem;
}
.headerButton {
  background: #000;
  color: #fff;
  border: none;
  padding: 0.5rem 1.5rem;
  margin: 0.5rem;
  border-radius: 0.5rem;
  cursor: pointer;
  text-decoration: none;
  font-family: inherit;
  text-align: center;
}
.headerButton:focus {
  outline: none;
}
.headerButton:active {
  transform: scale(0.98);
}
.headerButton {
  font-size: 1rem;
  height: 6.2rem;
  width: 6.2rem;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
.headerButton:hover {
  border: 4px solid orange;
}
.headerButton-block {
  display: block;
  width: 100%;
}
</style>
