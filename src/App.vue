<template>
  <div class="container" id="app">
    <v-app id="inspire">
      <HeaderComponent
        title="Task Tracker"
        @delete-all-tasks="deleteAllTasks"
        @add-task="addTask"
      />
      <TaskList
        :tasks="tasks"
        @delete-task="deleteTask"
        @mark-task-complete="markTaskComplete"
        @edit-task="editTask"
      />
    </v-app>
  </div>
</template>

<script>
import HeaderComponent from "./components/Template/HeaderComponent.vue";
import TaskList from "./components/Template/TaskList.vue";
export default {
  name: "App",
  components: { HeaderComponent, TaskList },
  data() {
    return {
      tasks: [],
    };
  },
  //Created is a method & lifecycle hook that is called when the component is first rendered. Also fetch API :D

  // You can make lifecycle components async!
  async created() {
    // when the component is created, check to see if localstorage has todolist items, if so set it to the tasks array, if not, fetch the API
    if (localStorage.getItem("todolist")) {
      this.tasks = JSON.parse(localStorage.getItem("todolist"));
    } else {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/todos"
      );
      const data = await response.json();
      this.tasks = data;
      localStorage.setItem("todolist", JSON.stringify(data));
    }
  },
  //when the task list changes, push the new tasks to local storage
  watch: {
    tasks: {
      handler() {
        localStorage.setItem("todolist", JSON.stringify(this.tasks));
      },
      deep: true,
    },
  },

  methods: {
    //When the user clicks the add task button,prompt the user for the name of the new task, and push it to the array with a unique id that starts at 0 and increments by 1
    addTask() {
      const taskName = prompt("What is the name of the task?");

      if (taskName.length > 70) {
        alert("Your task is too long! It must be less than 70 characters.");
      } else if (taskName.length === 0) {
        alert("You must have not have an empty task!");
      } else {
        this.tasks.push({
          id: this.tasks.length,
          title: taskName,
          completed: false,
        });
      }
    },

    deleteTask(id) {
      if (confirm("Are you sure you want to delete this task?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    deleteAllTasks() {
      if (confirm("Are you sure you want to delete all tasks?")) {
        this.tasks = [];
      }
    },
    markTaskComplete(id) {
      this.tasks.map((task) => {
        if (task.id === id) {
          task.completed = !task.completed;
        }
      });
    },
    editTask(id) {
      const task = this.tasks.find((task) => task.id === id);
      const updatedTask = prompt("Enter updated task", task.title);
      if (updatedTask.length > 70) {
        alert("Your task is too long! It must be less than 70 characters.");
      } else if (updatedTask.length === 0) {
        alert("You must have not have an empty task!");
      } else {
        task.title = updatedTask;
      }
    },
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 70rem;
  margin: 2rem auto;
  overflow: auto;
  min-height: 10rem;
  border: 1px solid steelblue;
  padding: 2rem;
  border-radius: 0.5rem;
}
</style>
