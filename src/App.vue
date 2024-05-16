<template>
  <div class="todo">
    <h1 class="todo__title">Todo list</h1>
    <form class="todo__form" action="/">
      <input class="todo__input" type="text" name="text" :value="taskValue" placeholder="Search note..."/>
      <select class="todo__select">
        <option value="all">All</option>
        <option value="complete">Complete</option>
        <option value="incomplete">Incomplete</option>
      </select>
      <button class="todo__theme-toggle" type="button"></button>
    </form>

    <ul class="todo__list">
      <li class="todo-list__item">
        <label>
          <input class="todo-list__checkbox" type="checkbox">
          <p>Купить продуктов</p>
        </label>
      </li>
      <li class="todo-list__item">
        <label>
          <input type="checkbox">
          <p>Заплатить за интернет</p>
        </label>
      </li>
    </ul>
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
input[type="text"] {
  width: 100%;
  box-sizing: border-box;
}

.todo {
  display: grid;
  grid-template-columns: 1fr 140px 54px;
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
  grid-column: 1 / -1;
  display: grid;
  grid-template-columns: 1fr 140px 54px;
  gap: 16px;
}

.todo__input {
  height: 38px;
  padding: 5px 10px;
  font-size: 16px;
  line-height: 20px;
  text-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
}

.todo__input::placeholder {
  color: #c3c1e5;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
}

.todo__select {
  font-size: 18px;
  line-height: 24px;
  font-weight: 500;
  color: #ffffff;
  border: none;
  text-transform: uppercase;
  background-color: #6c63ff;
}

.todo__select option {
  text-transform: lowercase;
  color: #000000;
  background-color: #ffffff;
}

.todo__theme-toggle {
  position: relative;
  display: flex;
  width: 38px;
  height: 38px;
  background-color: #6c63ff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  box-sizing: border-box;
}

.todo__theme-toggle::before {
  content: "";
  margin: auto;
  top: 0;
  left: 0;
  width: 22px;
  height: 22px;
  background-color: #ffffff;
  mask: url("/src/assets/moon.svg") no-repeat;
  mask-size: 100%;
}

.todo__list {
  grid-column: 1 / 2;
  margin: 0;
  padding: 0;
  list-style: none;
}

.todo-list__item label {
  display: flex;
  align-items: center;
  color: #252525;
  font-size: 20px;
  line-height: 24px;
}

.todo-list__checkbox {
  appearance: none;
  width: 26px;
  height: 26px;
  margin-right: 20px;
  border: 1px solid #6c63ff;
  border-radius: 2px;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
  cursor: pointer;
}

.todo-list__checbox:checked {
  background-color: #6c63ff;
}
</style>
