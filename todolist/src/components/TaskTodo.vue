<template>
  <div>
    <div class="task">
      <InputText type="text" v-model="valueTest" />
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
            @:keyup.enter="addTask"
            placeholder="Try typing 'Buy milk'"
            autocapitalize="off"
          />
          <input type="submit" class="submit" value="➡️" />
          <ul>
            <li v-for="(task, index) in tasks" :key="index">
              <input type="checkbox" v-model="index.completed" />
              <span :class="{ completed: task.completed }">{{
                task.text
              }}</span>
              <i class="pi pi-search" style="font-size: 2rem; color: black"></i>
              <button @click="deleteTask(index)">Clear All Tasks</button>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <button @click="clearCompleted">Clear Completed</button>
  </div>
</template>

<script>
import InputText from "primevue/inputtext";
import { ref } from "vue";

export default {
  name: "HelloWorld",
  components: {
    InputText,
  },
  props: {
    msg: String,
    value: String,
  },
  setup() {
    const valueTest = ref();
    return valueTest;
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
