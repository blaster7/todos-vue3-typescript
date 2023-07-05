<template>
  <footer class="app-footer">
    Активных задач: {{ statistics.active }}, сделано:{{ statistics.done }}
  </footer>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export interface Statistics {
  active: number;
  done: number;
}

export default defineComponent({
  props: {
    statistics: {
      type: Object as PropType<Statistics>,
      required: true,
    },
  },
});
</script>
