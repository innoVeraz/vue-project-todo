<script setup lang="ts">
import { Todo } from "../models/Todo";

//skapa ett propsobjekt som baseras på ett interface
interface ITodoViewProps {
  todo: Todo;
}

//ta emot egenskap från förälder med defineProps
const props = defineProps<ITodoViewProps>();

defineEmits<{ (e: "toggle", id: number): void }>();

// const handleClick = () => {
//   emits("toggle", props.todo.id);
// };
</script>

<template>
  <div
    @click="() => $emit('toggle', props.todo.id)"
    :class="props.todo.done ? 'done' : ''"
  >
    {{ props.todo.text }}
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
