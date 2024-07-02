<script setup>
import { ref, computed } from "vue";

const newId = ref(4);
const newTodo = ref("");

const todos = ref([
  {
    id: 1,
    name: "test",
    completed: false,
  },
  {
    id: 2,
    name: "hue",
    completed: false,
  },
  {
    id: 3,
    name: "kaiser",
    completed: false,
  },
]);

const showCompleted = ref(true);
const filteredTodos = computed(() => {
  return showCompleted.value
    ? todos.value
    : todos.value.filter((todo) => !todo.completed);
});

function addTodo() {
  todos.value.push({
    id: newId.value++,
    name: newTodo.value,
    completed: false,
  });
  newTodo.value = "";
}

const removeTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};
</script>

<template>
  <div class="flex justify-center">
    <div class="h-screen bg-slate-500 pt-5 w-1/4">
      <div
        class="mx-auto w-max flex items-center border-b border-red-600 border-opacity-25 hover:border-opacity-100 transition ease-in-out delay-150"
      >
        <input
          v-model="newTodo"
          class="appearance-none bg-transparent border-none text-black mr-3 py-1 px-2 leading-tight focus:outline-none"
          type="text"
          placeholder="Add Todo"
          aria-label="Todo name"
        />
        <button class="border-black" @click="addTodo">Add</button>
      </div>
      <div class="grid row-span-1">
        <p v-for="todo in filteredTodos" :id="todo.id" class="mx-auto">
          <span :class="todo.completed ? 'line-through' : ''">
            {{ todo.name }}
          </span>
          <button
            @click="removeTodo(todo.id)"
            class="w-8 h-8 m-2 border-2 border-black border-r-2"
          >
            X
          </button>
          <button
            @click="todo.completed = !todo.completed"
            class="w-20 h-8 m-2 border-2 border-black border-r-2"
          >
            Complete
          </button>
        </p>

        <div class="mx-auto">
          <button @click="showCompleted = !showCompleted">
            {{ showCompleted ? "Hide" : "Show" }} completed todos
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
