<template>
  <section class="add-todo">
    <form
      v-if="istFormVisible"
      class="add-todo__form"
      @submit.prevent="submitForm"
    >
      <button class="close-button" type="button" @click.stop="toggleForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Добавить задачу</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="toggleForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import { Todo } from "@/types/Todo";
import { defineComponent } from "vue";

interface State {
  istFormVisible: boolean;
  todoText: string;
}

export default defineComponent({
  data(): State {
    return {
      istFormVisible: false,
      todoText: "",
    };
  },
  emits: {
    addTodo: (todo: Todo) => todo,
  },
  methods: {
    toggleForm() {
      this.istFormVisible = !this.istFormVisible;
    },
    submitForm() {
      this.$emit("addTodo", {
        id: Date.now(),
        text: this.todoText,
        completed: false,
      });
      this.todoText = "";
      this.toggleForm();
    },
  },
});
</script>
