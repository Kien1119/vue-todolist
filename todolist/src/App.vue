<template>
  <TaskTodo msg="📋 My tasks" />
</template>

<script>
import TaskTodo from "./components/TaskTodo.vue";
import "primeicons/primeicons.css";
export default {
  name: "App",
  components: {
    TaskTodo,
  },
};
</script>

<style>
body {
  /* background: #222; */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}

.new-task-form {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: white;
  background: #333;
  padding: calc(2 * 0.5rem);
  border-radius: calc((0.5rem));
  width: calc(100% - 4 * 0.5rem);
  max-width: 50rem;
  border: 1px solid #333;
  margin-left: calc(30% - 4 * 0.5rem);
}
.new-task-form:hover {
  background-color: #444;
  border: 1px solid white;
}
#new-task {
  width: 568px;
  height: 40px;
  position: relative;
  opacity: 0;
  padding: 0.5rem;
  flex: 1;
  color: white;
  border-radius: 10px;
  margin-right: 10px;
  margin-left: 10px;
}
#new-task:focus {
  opacity: 1;
  outline: none;
  background: #333;
  border: none;
}

.submit {
  border: none;
  margin: 0;
  padding: 0;
  background: transparent;
  font-family: inherit;
  font-size: inherit;
}
button {
  float: right;
  margin-left: 0;
  margin-right: 22%;
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 1em;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background: var(--task-background);
  color: white;
}
</style>
