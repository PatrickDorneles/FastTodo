<template>
  <div class="app-container">
    <app-title />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppTitle from "./components/AppTitle.vue";

const App = defineComponent({
  name: "App",
  components: {
    AppTitle,
  },
});

export default App;
</script>

<style lang="scss" scoped>
.app-container {
  height: 100vh;
  width: 100vw;
  background-color: #fff8e1;
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
