<template>
  <TheHeader />
  <TheFilters :active-filter="activeFilter" @set-filter="setFilter" />
  <main class="app-main">
    <TheTodoList
      :todos="filterTodos"
      @toggle-todo="toggleTodo"
      @delete-todo="deleteTodo"
    />
    <TheAddTodo @add-todo="addTodo" />
  </main>
  <TheFooter :statistics="statistics" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TheHeader from "@/components/TheHeader.vue";
import TheFilters from "@/components/TheFilters.vue";
import TheTodoList from "@/components/TheTodoList.vue";
import TheAddTodo from "@/components/TheAddTodo.vue";
import TheFooter, { Statistics } from "@/components/TheFooter.vue";
import { Todo } from "@/types/Todo";
import { Filter } from "@/types/Filter";

interface State {
  todos: Todo[];
  activeFilter: Filter;
}

export default defineComponent({
  components: { TheHeader, TheFilters, TheTodoList, TheAddTodo, TheFooter },
  data(): State {
    return {
      todos: [
        { id: 0, text: "Изучить основы Vue", completed: true },
        { id: 1, text: "Изучить основы Typescript", completed: true },
        { id: 2, text: "Выполнить домашнее задание", completed: false },
      ],
      activeFilter: "Все",
    };
  },
  computed: {
    filterTodos(): Todo[] {
      switch (this.activeFilter) {
        case "В работе":
          return this.activeTodos;
        case "Готовы":
          return this.doneTodos;
        case "Все":
        default:
          return this.todos;
      }
    },
    statistics(): Statistics {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length,
      };
    },
    activeTodos(): Todo[] {
      return this.todos.filter((todo) => !todo.completed);
    },
    doneTodos(): Todo[] {
      return this.todos.filter((todo) => todo.completed);
    },
  },
  methods: {
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id);
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
      }
    },
    deleteTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
    },
    addTodo(todo: Todo) {
      this.todos.push(todo);
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter;
    },
  },
});
</script>
