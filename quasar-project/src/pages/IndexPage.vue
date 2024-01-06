<template>
  <q-page class="flex flex-center">
    <TodoList />
  </q-page>
</template>

<script>
import TodoList from 'components/TodoList.vue';

export default {
  components: {
    TodoList,
  },
};
</script>
