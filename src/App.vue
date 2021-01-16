<template>
  <div id="app">
    <img src="./assets/logo.png" />
    <todoList />
  </div>
</template>

<script>
import todoList from "./components/TodoList";

export default {
  name: "App",
  components: {
    todoList
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
