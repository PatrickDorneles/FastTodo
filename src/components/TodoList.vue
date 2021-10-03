<template>
  <div class="todo-container">
    <div class="insert-task-container">
      <input
        type="text"
        class="insert-task"
        v-model="taskToInsert"
        placeholder="Write your task here"
        @keydown.enter="addTask"
      />
      <button class="add-task" @click="addTask">
        <add-task-icon />
      </button>
    </div>
    <ul class="task-list">
      <task
        v-for="task in tasks"
        :key="task.id"
        :id="task.id"
        :name="task.name"
        :done="task.done"
        @delete-task="deleteTask"
        @change-status="changeStatus"
        @edit-name="editName"
      />
    </ul>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import AddTaskIcon from "./svg/AddTaskIcon.vue";
import Task from "./Task.vue";

export default defineComponent<{
  taskToInsert: string;
  tasks: { id: number; done: boolean; name: string }[];
  taskIndex: number;
}>({
  components: { AddTaskIcon, Task },
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
      this.taskToInsert = "";
    },
    deleteTask(id: number) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    changeStatus(id: number) {
      const task = this.tasks.find((task) => task.id === id);
      if (task) task.done = !task.done;
    },
    editName(edited: { id: number; name: string }) {
      const task = this.tasks.find((task) => task.id === edited.id);
      if (task) task.name = edited.name;
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
      font-size: 1em;

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

  .task-list {
    display: flex;
    flex-direction: column;
    margin-top: 20px;
    list-style-type: none;
    gap: 8px;

    height: 50vh;
    overflow: auto;

    &::-webkit-scrollbar {
      width: 4px;
    }

    &::-webkit-scrollbar-track {
      background: #fff8e1;
    }

    &::-webkit-scrollbar-thumb {
      background: #9fa8da;
    }

    &::-webkit-scrollbar-thumb:hover {
      background: #5c6bc0;
    }
  }
}
</style>
