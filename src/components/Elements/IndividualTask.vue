<template>
  <div :class="[task.completed ? 'reminder' : '', 'IndividualTask']">
    <div class="TaskContainer">
      <h3 class="TaskTitle">{{ task.title }}</h3>
      <i class="fas fa-times" @click="$emit('delete-task', task.id)"></i>
      <i class="fas fa-edit" @click="$emit('edit-task', task.id)"></i>
      <i class="fas fa-check" @click="$emit('mark-task-complete', task.id)"></i>

      <v-tooltip bottom color="success">
        <template v-slot:activator="{ on, attrs }">
          <i
            class="fas fa-trash-alt"
            @click="$emit('delete-task', task.id)"
            :on="on"
            :attrs="attrs"
          ></i>
        </template>
        <span>Delete Button</span>
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
