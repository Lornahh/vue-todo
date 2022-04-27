<template>
  <div :class="[task.completed ? 'reminder' : '', 'IndividualTask']">
    <div class="TaskContainer">
      <h3 class="TaskTitle">{{ task.title }}</h3>

      <v-tooltip anchor="bottom">
        <template v-slot:activator="{ props }">
          <i
            class="fas fa-edit"
            v-bind="props"
            @click="$emit('edit-task', task.id)"
          ></i>
        </template>
        <span>Edit This task...</span>
      </v-tooltip>

      <v-tooltip anchor="bottom">
        <template v-slot:activator="{ props }">
          <i
            class="fas fa-times"
            v-bind="props"
            @click="$emit('delete-task', task.id)"
          ></i>
        </template>
        <span>Delete This Task...</span>
      </v-tooltip>

      <v-tooltip anchor="bottom">
        <template v-slot:activator="{ props }">
          <i
            class="fas fa-check"
            v-bind="props"
            @click="$emit('mark-task-complete', task.id)"
          ></i>
        </template>
        <span>Mark This Task Complete...</span>
      </v-tooltip>
    </div>

    <p v-if="task.completed">This task is completed!</p>
    <p v-else>This task is not completed!</p>
  </div>
</template>

Line 2 is a a very weird move. V-bind class is used, and based off the
truthiness of task.completed, it may append '.reminder' onto the end of the
class name. The other string is set to empty because if it isnt true, we want
the class to stay the same, "IndividualTask"

<script>
export default {
  name: "IndividualTask",
  props: {
    task: {
      type: Object,
      default: null,
    },
  },
};
//FAS is the delete button.
</script>

<style scoped>
.fa-check {
  color: green;
}
.fa-times {
  color: red;
}
.fa-edit {
  color: blue;
}
.TaskTitle {
  width: 69rem;
}
.TaskContainer {
  display: flex;
  align-items: center;
  justify-content: left;
  column-gap: 1.2rem;
}

.IndividualTask {
  background: #f4f4f4;
  margin: 0.5rem;
  padding: 0.5rem 1.5rem;
}
.IndividualTask.reminder {
  border-left: 0.5rem solid green;
}
</style>
