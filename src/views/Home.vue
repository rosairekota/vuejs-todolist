<template>
  <div class="home">
    <TodoList/>
  </div>
</template>

<script>
// @ is an alias to /src
import TodoList from "@/components/todo/Todos.vue";

export default {
  name: "Home",
  components: {
    TodoList,
  },
};
</script>
