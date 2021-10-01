<template>
  <div class="title-container">
    <fast-todo-title-logo class="title-logo" />
    <span>Your fastest todo application!</span>
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
  display: flex;

  flex-direction: column;
  align-items: center;
  justify-content: center;

  gap: 40px;

  margin-top: 50px;
  width: 100vw;

  .title-logo {
    transform: scale(4) translateX(-2px);
  }

  span {
    font-family: "Noto Sans Display", sans-serif;
    color: #283593;
  }
}
</style>
