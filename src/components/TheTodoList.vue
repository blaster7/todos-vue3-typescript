<template>
  <ul class="todo-list">
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle-todo="toggleTodo"
      @delete-todo="deleteTodo"
    />
  </ul>
</template>

<script lang="ts">
import { PropType, defineComponent } from "vue";
import TodoItem from "@/components/TodoItem.vue";
import { Todo } from "@/types/Todo";

export default defineComponent({
  components: { TodoItem },
  props: {
    todos: {
      type: Array as PropType<Todo[]>,
    },
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    deleteTodo: (id: number) => Number.isInteger(id),
  },
  methods: {
    toggleTodo(id: number) {
      this.$emit("toggleTodo", id);
    },
    deleteTodo(id: number) {
      this.$emit("deleteTodo", id);
    },
  },
});
</script>
