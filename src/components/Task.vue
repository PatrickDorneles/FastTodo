<template>
  <li class="task-container">
    <label class="check-container">
      <input type="checkbox" v-bind:checked="done" @change="changeStatus" />
      <span class="checkmark"></span>
    </label>
    <span
      class="task-name"
      v-bind:class="done ? 'done' : ''"
      @click="changeStatus"
      v-if="!edit"
    >
      {{ name }}
    </span>
    <input
      class="edit-input"
      v-if="edit"
      v-model="editName"
      v-bind:focus="edit"
      @keydown.enter="completeEditing"
    />
    <button
      class="edit"
      v-bind:class="edit ? 'active' : ''"
      @click="changeEditMode"
    >
      <edit-task-icon />
    </button>
    <button class="delete" @click="deleteTask">
      <delete-task-icon />
    </button>
  </li>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import DeleteTaskIcon from "./svg/DeleteTaskIcon.vue";
import EditTaskIcon from "./svg/EditTaskIcon.vue";
export default defineComponent({
  components: { DeleteTaskIcon, EditTaskIcon },

  data: function () {
    return {
      edit: false,
      editName: this.name,
    };
  },
  props: {
    id: Number,
    name: String,
    done: Boolean,
  },
  methods: {
    deleteTask() {
      this.$emit("deleteTask", this.id);
    },
    changeStatus() {
      this.$emit("changeStatus", this.id);
    },
    changeEditMode() {
      this.edit = !this.edit;

      if (this.editName !== this.name) {
        this.$emit("editName", { id: this.id, name: this.editName });
      }
    },
    completeEditing() {
      this.$emit("editName", { id: this.id, name: this.editName });
      this.edit = false;
    },
  },
});
</script>
<style lang="scss" scoped>
li.task-container {
  display: flex;
  align-items: center;

  border-bottom: 1px solid #7986cb;

  .check-container {
    position: relative;
    height: 25px;
    padding-left: 35px;
    cursor: pointer;
    font-size: 22px;
    user-select: none;

    input {
      position: absolute;
      opacity: 0;
      cursor: pointer;
      height: 0;
      width: 0;
    }

    .checkmark {
      top: 0;
      left: 0;
      height: 25px;
      width: 25px;
      background: transparent;

      &:after {
        content: "";
        position: absolute;
        display: none;
      }

      &:after {
        left: 9px;
        top: 5px;
        width: 5px;
        height: 10px;
        border: solid #43a047;
        border-width: 0 3px 3px 0;
        -webkit-transform: rotate(45deg);
        -ms-transform: rotate(45deg);
        transform: rotate(45deg);
      }
    }

    input:checked ~ .checkmark:after {
      display: block;
    }
  }

  .task-name {
    flex: 1;
    text-align: start;
    user-select: none;
    cursor: pointer;

    font-family: "Noto Sans Display", sans-serif;
    font-size: 1em;

    &.done {
      text-decoration: line-through;
    }
  }

  .edit-input {
    flex: 1;

    font-family: "Noto Sans Display", sans-serif;
    font-size: 1em;

    border: none;
  }

  button {
    background: none;
    border: none;

    cursor: pointer;

    &.active {
      svg {
        fill: #43a047;
      }
    }

    svg {
      fill: #7986cb;
    }

    &:active svg {
      fill: blue;
    }
  }
}
</style>
