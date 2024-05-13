<template>
  <div class="todo-list">
    <form action="/">
      <input type="text" name="text" :value="taskValue" />
      <button @click="addTask" type="submit">Добавить</button>
    </form>

    <ol class="todo-list">
      <li class="todo-list__item">Купить продуктов</li>
      <li class="todo-list__item">Заплатить за интернет</li>
    </ol>
  </div>
</template>

<script>
export default {
  data() {
    return {
    };
  },
  methods: {
    addTask(event) {
      console.log(event);
    }
  },
};
</script>


<style scoped></style>
