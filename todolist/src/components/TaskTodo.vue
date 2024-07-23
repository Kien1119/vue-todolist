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
        <li class="divider">{{ resolveTaskText }}</li>
      </ul>
      <ul id="taskCheck" v-if="tasks.length > 0">
        <li class="task-li" v-for="(task, index) in tasks" :key="index">
          <input class="checkbox" type="checkbox" v-model="task.completed" />
          <span
            v-if="editIndex !== index"
            :class="task.completed ? 'task_complete' : ''"
          >
            {{ task.text }}
          </span>
          <input type="text" v-else v-model="editData" />
          <button
            v-if="editIndex == index"
            @click="cancelTask(task.text, index)"
          >
            <i class="pi pi-times" style="color: red"></i>
          </button>
          <button @click="updateTask(task.text, index)">
            <i
              class="pi pi-user-edit"
              style="color: white; margin-right: 5px"
            ></i>
          </button>
          <button v-if="editIndex == index" @click="ediTask()">
            <i class="pi pi-check" style="color: green"></i>
          </button>
          <button class="deleteTask" @click="deleteTask(index)">
            Delete task
          </button>
        </li>
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
      editIndex: -1,
      editData: "",
    };
  },
  components: {
    //InputText,
  },
  mounted() {
    const savedTasks = localStorage.getItem("tasks");
    if (savedTasks) {
      try {
        this.tasks = JSON.parse(savedTasks);
      } catch (e) {
        console.error("Error parsing tasks from localStorage", e);
      }
    }
  },
  computed: {
    resolveTaskText() {
      if (this.tasks.length === 0) {
        return "No tasks defined";
      }
      if (this.tasks.length > 0 && !this.tasks.every((t) => t.completed)) {
        return "To do";
      }
      if (
        this.tasks.length > 0 &&
        this.tasks.filter((task) => !task.completed)
      ) {
        return "Completed";
      } else {
        return ` ${this.tasks.filter((task) => !task.completed)} Completed`;
      }
    },
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
    updateTask(text, index) {
      this.editData = text;
      this.editIndex = index;
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
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
    cancelTask() {
      this.editIndex = -1;
      this.editData = "";
      alert("Cancle Success");
    },

    ediTask() {
      this.tasks.forEach((data, index) => {
        if (this.editIndex === index) {
          data.text = this.editData;
          console.log(data);
        }
      });
      this.editIndex = -1;
      this.editData = "";
      console.log(this.tasks);
      this.saveTasks();
    },
  },

  props: {
    msg: String,
    value: String,
  },
};
</script>

<style scoped>
.task_complete {
  color: #222;
  text-decoration: line-through;
}
</style>
