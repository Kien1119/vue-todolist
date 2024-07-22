<template>
  <div>
    <div class="task">
      <h1>{{ msg }}</h1>
      <label for="new-task"></label>
      <div class="tasks">
        <div class="new-task-form">
          <label for="new-task-form">➕ Add a task</label>
          <input
            type="text"
            name=""
            id="new-task"
            v-model="newTask"
            @keyup.enter="addTask"
            placeholder="Try typing 'Buy milk'"
            autocapitalize="off"
          />
          <input type="submit" @click="addTask" class="submit" value="➡️" />
        </div>
      </div>
      <ul id="divider">
        <li class="divider">No tasks defined</li>
      </ul>
      <ul id="taskCheck" v-if="tasks.length > 0">
        <li class="task-li" v-for="(task, index) in tasks" :key="index">
          <input class="checkbox" type="checkbox" v-model="index.completed" />
          <span :class="{ completed: task.completed }">{{ task.text }}</span>
        </li>
        <button class="deleteTask" @click="deleteTask(index)">
          Delete task
        </button>
      </ul>
    </div>
    <button @click="clearCompletedTask">
      <i class="pi pi-trash" style="color: white; margin-right: 5px"></i>Clear
      Completed
    </button>
    <button @click="clearAll">
      <i class="pi pi-trash" style="color: white; margin-right: 5px"></i>Clear
      All
    </button>
  </div>
</template>

<script>
// import InputText from "primevue/inputtext"; -->
// import { ref } from "vue";

export default {
  name: "TaskTodo",
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  components: {
    //InputText,
  },
  mounted() {
    this.loadTask();
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        const newTask = { text: this.newTask.trim(), completed: false };
        this.tasks.push(newTask);
        this.saveTasks();
        this.newTask = "";
      }
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    loadTasks() {
      const savedTasks = localStorage.getItem("tasks");
      if (savedTasks) {
        try {
          this.tasks = JSON.parse(savedTasks);
        } catch (e) {
          console.error("Error parsing tasks from localStorage", e);
        }
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasks();
    },
    clearCompletedTask() {
      this.tasks = this.tasks.filter((task) => !task.completed);
      this.saveTasks();
    },
    clearAll() {
      this.tasks = [];
      this.saveTasks();
    },
  },
  props: {
    msg: String,
    value: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
