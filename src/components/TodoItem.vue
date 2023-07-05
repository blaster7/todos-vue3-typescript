<template>
  <li
    class="todo-item"
    :class="{ 'todo-item--done': todo.completed }"
    @click="toggleTodo"
  >
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="deleteTodo">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<script lang="ts">
import { Todo } from "@/types/Todo";
import { defineComponent, PropType } from "vue";

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true,
    },
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    deleteTodo: (id: number) => Number.isInteger(id),
  },
  methods: {
    toggleTodo() {
      this.$emit("toggleTodo", this.todo.id);
    },
    deleteTodo() {
      this.$emit("deleteTodo", this.todo.id);
    },
  },
});
</script>
