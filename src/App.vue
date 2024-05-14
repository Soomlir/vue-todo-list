<template>
  <div class="todo">
    <h1 class="todo__title">Todo list</h1>
    <form class="todo__form" action="/">
      <input class="todo__input" type="text" name="text" :value="taskValue" />
      <select>
        <option value="all">All</option>
        <option value="complete">Complete</option>
        <option value="incomplete">Incomplete</option>
      </select>
    </form>

    <button></button>

    <ol class="todo__list">
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


<style scoped>
.todo {
  display: grid;
  grid-template-columns: 595px 85px 38px;
  width: 750px;
  margin-right: auto;
  margin-left: auto;
}

.todo__title {
  grid-column: 1 / -1;
  font-size: 26px;
  line-height: 30px;
  text-transform: uppercase;
  color: #252525;
  text-align: center;
}

.todo__form {
  grid-column: 1 / 3;
  display: flex;
}

.todo__input {
  min-width: 595px;
}

.todo__list {
  grid-column: 1 / -1;
}
</style>
