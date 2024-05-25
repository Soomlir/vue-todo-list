<template>
  <div class="todo-wrapper">
    <div class="todo">
      <h1 class="todo__title">Todo list</h1>
      <form class="todo__form" action="/">
        <input
          class="todo__input"
          type="text"
          name="text"
          placeholder="Search note..."
          v-model="searchFilter"
        />
        <select class="todo__select" v-model="searchMode">
          <option
            v-for="mode in searchModes"
            :key="mode"
            :selected="mode === searchMode"
          >
            {{ mode }}
          </option>
        </select>
        <button class="todo__theme-toggle" type="button"></button>
      </form>

      <ul class="todo__list" v-if="filteredTodos.length">
        <li
          class="todo-list__item"
          v-for="(item, i) in filteredTodos"
          :key="item.id"
        >
          <label>
            <input
              class="todo-list__checkbox"
              type="checkbox"
              v-model="item.done"
            />
            <p>{{ item.task }}</p>
          </label>
          <button
            @click="openModal(i)"
            class="todo-list__edit"
            type="button"
          >
            <span class="visually-hidden">Редактировать запись.</span>
          </button>
          <button
            @click="deleteNote(item.id)"
            class="todo-list__delete"
            type="button"
          >
            <span class="visually-hidden">Удалить запись.</span>
          </button>
        </li>
      </ul>
      <p v-else>Дела не найдены.</p>
    </div>
    <button class="todo__new-post" @click="openModal(-1)" type="button">
      <span class="visually-hidden">Создать новую заметку.</span>
    </button>
  </div>

  <div class="modal" :class="{ 'modal--show': modalShow }">
    <div class="modal__content">
      <h2 class="modal__title">{{ isEditMode ? 'Редактировать' : 'Добавить' }} заметку</h2>
      <form>
        <input
          class="modal__input"
          type="text"
          placeholder="Input your note..."
          v-model.trim="inputValue"
        />
        <button @click="applyValue" class="modal__apply" type="button">
          Apply
        </button>
        <button class="modal__cancel" @click="closeModal" type="button">
          Cancel
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      modalShow: false,
      inputValue: "",
      todos: [{ id: 1, task: "Купить продуктов", done: false }],
      id: 2,
      searchModes: ["all", "complete", "incomplete"],
      searchMode: "all",
      searchText: "",
      searchFilter: "",
      indexOfEdited: -1,
    };
  },
  methods: {
    openModal(i) {
      this.indexOfEdited = i;
      if (i > -1) {
        this.inputValue = this.todos[i].task;
      }
      this.modalShow = true;
    },

    closeModal() {
      this.inputValue = "";
      this.modalShow = false;
    },

    applyValue() {
      if (this.isEditMode) {
        const currentNote = this.todos[this.indexOfEdited];
        if (this.inputValue === "") {
          this.deleteNote(currentNote.id);
        } else {
          currentNote.task = this.inputValue;
        }
      } else if (this.inputValue !== "") {
        this.todos.push({
          id: ++this.id,
          task: this.inputValue,
          done: false,
        });
      }
      this.closeModal();
    },

    deleteNote(id) {
      this.todos = this.todos.filter((elem) => elem.id !== id);
    },
  },
  computed: {
    isEditMode() {
      return this.indexOfEdited > -1;
    },
    filteredTodos() {
      return this.todos.filter(({ done, task }) => {
        const searchCondition = this.searchFilter
          ? task.toLowerCase().includes(this.searchFilter)
          : true;
        if (this.searchMode === "complete") {
          return done && searchCondition;
        }
        if (this.searchMode === "incomplete") {
          return !done && searchCondition;
        }
        return searchCondition;
      });
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  z-index: 1000;
  display: none;
  inset: 0;
  overflow: scroll;
  overflow-x: scroll;
  overflow-x: hidden;
}

.modal--show {
  display: flex;
}

.modal__content {
  position: relative;
  width: 450px;
  height: 289px;
  margin: auto;
  padding: 30px;
  background-color: #fff;
  outline: 1px solid #c6c6c6;
  box-shadow: 0 5px 10px #00010140;
}

.modal__title {
  text-transform: uppercase;
  text-align: center;
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

.todo-wrapper {
  width: 750px;
  margin-right: auto;
  margin-left: auto;
}

.todo {
  display: grid;
  grid-template-columns: 1fr 140px 54px;
  margin-bottom: 40px;
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

.todo-list__checkbox:checked + p {
  color: rgba(0, 0, 0, 0.3);
  text-decoration: line-through;
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
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 24px;
  height: 24px;
  background-image: url("../src/assets/plus.svg");
}

.modal form {
  display: flex;
  flex-wrap: wrap;
}

.modal__input {
  flex-grow: 1;
  padding: 10px;
  font-size: 16px;
  font-weight: 500;
  border: 1px solid #6c63ff;
  border-radius: 5px;
}

.modal__apply,
.modal__cancel {
  width: 110px;
  padding: 10px 20px;
  margin-top: 120px;
  font-weight: 500;
  text-transform: uppercase;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.modal__apply {
  color: #ffffff;
  background-color: #6c63ff;
}

.modal__apply:focus,
.modal__apply:hover {
  background-color: rgba(108, 99, 255, 0.6);
}

.modal__apply:active {
  background-color: rgba(108, 99, 255, 0.3);
}

.modal__cancel {
  margin-left: auto;
  color: #6c63ff;
  background-color: #ffffff;
  border: 1px solid #6c63ff;
}

.modal__cancel:focus,
.modal__cancel:hover {
  background-color: rgba(108, 99, 255, 0.6);
  color: #ffffff;
}

.modal__cancel:active {
  color: #ffffff;
  background-color: rgba(108, 99, 255, 0.3);
}
</style>
