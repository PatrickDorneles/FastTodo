<template>
  <div class="title-container">
    <fast-todo-title-logo class="title-logo" />
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import FastTodoTitleLogo from "./svg/FastTodoTitleLogo.vue";

export default defineComponent({
  components: {
    FastTodoTitleLogo,
  },
});
</script>

<style lang="scss" scoped>
.title-container {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;

  top: 40px;
  width: 100vw;
  .title-logo {
    transform: scale(4) translateX(-3px);
  }
}
</style>
