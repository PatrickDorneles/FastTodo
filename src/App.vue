<template>
  <div class="app-container">
    <app-title />
    <todo-list />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppTitle from "./components/AppTitle.vue";
import TodoList from "./components/TodoList.vue";

const App = defineComponent({
  name: "App",
  setup() {
    const todoIndex = localStorage.getItem("todoIndex");

    if (!todoIndex) {
      localStorage.setItem("todoIndex", "0");
    }
  },
  components: {
    AppTitle,
    TodoList,
  },
});

export default App;
</script>

<style lang="scss" scoped>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;

  height: 100vh;
  width: 100vw;
  background-color: #fff8e1;

  gap: 40px;
}
</style>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
