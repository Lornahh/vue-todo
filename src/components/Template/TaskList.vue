<template>
  <div>
    <ul v-for="task in tasks" :key="task.id" class="TaskList">
      <li class="IndividualTask">
        <IndividualTask
          :task="task"
          @delete-task="$emit('delete-task', task.id)"
          @mark-task-complete="$emit('mark-task-complete', task.id)"
          @edit-task="$emit('edit-task', task.id)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import IndividualTask from "../Elements/IndividualTask";
export default {
  name: "TaskList",
  props: {
    tasks: {
      type: Array,
      default: null,
    },
  },
  components: { IndividualTask },
};
</script>

<style scoped>
.TaskList {
  list-style: none;
  padding: 0;
}
</style>
