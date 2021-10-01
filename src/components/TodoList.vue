<template>
  <div class="todo-container">
    <div class="insert-task-container">
      <input
        type="text"
        class="insert-task"
        v-model="taskToInsert"
        placeholder="Write your task here"
      />
      <button class="add-task" v-on:click="addTask">
        <add-task-icon />
      </button>
    </div>
    <span v-for="task in tasks" :key="task.id">
      {{ task.name }}
    </span>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import AddTaskIcon from "./svg/AddTaskIcon.vue";

export default defineComponent<{
  taskToInsert: string;
  tasks: { id: number; done: boolean; name: string }[];
  taskIndex: number;
}>({
  components: { AddTaskIcon },
  data: function () {
    return {
      taskToInsert: "",
      tasks: [],
      taskIndex: 0,
    };
  },
  methods: {
    addTask() {
      if (this.taskToInsert === "") return;
      const taskToAdd = {
        id: this.taskIndex++,
        done: false,
        name: this.taskToInsert,
      };
      this.tasks.push(taskToAdd);
    },
  },
});
</script>

<style lang="scss" scoped>
.todo-container {
  display: flex;
  flex-direction: column;

  width: 350px;

  .insert-task-container {
    display: flex;
    gap: 10px;

    width: 100%;

    .insert-task {
      flex: 1;
      border: none;
      border-bottom: 1px solid #7986cb;
      background: none;
      outline: none;

      font-family: "Noto Sans Display", sans-serif;
      font-size: 1.2em;

      color: #1565c0;
    }

    .add-task {
      background: none;
      border: none;

      cursor: pointer;

      svg {
        fill: #7986cb;
      }

      &:active svg {
        fill: blue;
      }
    }
  }
}
</style>
