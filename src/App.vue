<template>
  <div class="todo">
    <h1 class="todo__title">Todo list</h1>
    <form class="todo__form" action="/">
      <input
        class="todo__input"
        type="text"
        name="text"
        placeholder="Search note..."
      />
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
          <input class="todo-list__checkbox" type="checkbox" />
          <p>Купить продуктов</p>
        </label>
        <button class="todo-list__edit" type="button">
          <span class="visually-hidden">Редактировать запись.</span>
        </button>
        <button class="todo-list__delete" type="button">
          <span class="visually-hidden">Удалить запись.</span>
        </button>
      </li>
    </ul>
  </div>
  <button class="todo__new-post" @click="addNewNote" type="button">
    <span class="visually-hidden">Создать новую заметку.</span>
  </button>

  <div class="modal">
    <div class="modal-content">
      <h2>New Note</h2>
      <form action="/">
        <input type="text" placeholder="Input your note..." />
        <button type="submit">Apply</button>
        <button type="button">Cancel</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      abcd: "sss",
    };
  },
  methods: {
    addNewNote() {
      console.log(123);
      // получить див modal
      // включить класс Modal--show
      // стилизовать модальное окошко
      // реализовать ESC и клик вне окошка
    }
  },
};
</script>

<style scoped>
.modal {
  display: none;
}

.modal--show {
  display: flex;
}

.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  border: 0;
  clip: rect(0 0 0 0);
}

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
  margin-bottom: 40px;
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
  padding-left: 10px;
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

.todo-list__item {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #6c63ff;
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

.todo-list__checkbox:checked {
  background-image: url("src/assets/checkbox-on.svg");
  background-repeat: no-repeat;
  background-position: center;
  background-color: #6c63ff;
}

.todo-list__edit,
.todo-list__delete {
  position: relative;
  display: inline-block;
  width: 18px;
  height: 18px;
  border: none;
  background-color: transparent;
  cursor: pointer;
}

.todo-list__edit {
  margin-right: 20px;
  margin-left: auto;
}

.todo-list__edit::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 18px;
  height: 18px;
  background-image: url("src/assets/pencil.svg");
  background-repeat: no-repeat;
  background-position: center;
}

.todo-list__delete {
  margin-right: 20px;
}

.todo-list__delete::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 18px;
  height: 18px;
  background-image: url("src/assets/trash.svg");
  background-repeat: no-repeat;
  background-position: center;
}

.todo__new-post {
  position: relative;
  width: 50px;
  height: 50px;
  background: #6c63ff;
  border: none;
  border-radius: 50%;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
  cursor: pointer;
}

.todo__new-post::before {
  content: "";
  position: absolute;
  top: 11px;
  left: 13px;
  width: 24px;
  height: 24px;
  background-image: url("../src/assets/plus.svg");
}
</style>
