<template>
  <div class="sidebar">
    <div class="sidebar-list">
      <div class="list">
        <button class="sidebar-button">
          <img src="@/assets/img/Vector.svg" alt="" />
        </button>
        <span>{{ titleSidebar }}</span>
      </div>

      <div class="sidebar-toDo" v-for="todo in todoList" :key="todo.id">
        <div class="sideleft">
          <div class="circle"></div>
          <span>{{ todo.name }}</span>
        </div>

        <button class="button-cancel" @click="delltodo(todo.id)">
          <img src="@/assets/img/cancel.svg" alt="" />
        </button>
      </div>

      <div class="add-list">
        <button class="plusbutton" @click="modal = true">
          <span class="sidebar__plus">+</span>
        </button>

        <span class="sidebar-text-add">Добавить папку</span>

        <div class="sidebar-modal" v-show="modal === true">
          <button class="model-cancel" @click="modal = false">
            <i class="fa fa-times"></i>
          </button>
          <form @submit.prevent="addTodo">
            <input type="text" placeholder="Название папки" v-model="command" />
            <div class="circle_change">
              <div class="child-circle"></div>
              <div class="child-circle"></div>
              <div class="child-circle"></div>
              <div class="child-circle"></div>
              <div class="child-circle"></div>
              <div class="child-circle"></div>
              <div class="child-circle"></div>
              <div class="child-circle"></div>
            </div>
            <button class="addbutton">Добавить</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
let id = 1;
export default {
  data() {
    return {
      modal: false,
      titleSidebar: "Все задачи",
      command: "",
      todoList: [
        { id: id++, name: "Покупки" },
        { id: id++, name: "Фронтенд" },
        { id: id++, name: "Фильмы и" },
        { id: id++, name: "Книги" },
        { id: id++, name: "Личное" },
      ],
    };
  },

  methods: {
    addTodo() {
      if (this.command === "") {
        return;
      }

      this.todoList.push({
        name: this.command,
      });

      this.command = "";
    },
    delltodo(id) {
      let index = this.todoList.findIndex((todo) => todo.id === id);
      this.todoList.splice(index, 1);
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.sidebar {
  width: 230px;
  max-width: 100%;
  height: 100vh;
  background-color: #e5e5e5;
  padding: 0px 30px;
}

.sidebar-button {
  border: none;
  background: none;
}
.sidebar-button img {
  width: 20px;
  height: 20px;
}
.list {
  display: flex;
  gap: 9px;

  padding-top: 56px;
  margin-bottom: 40px;
}
.list span {
  font-size: 19px;
}
.sidebar-toDo {
  width: 170px;

  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 12px;
  transition: all 0.2s ease;
}
.sidebar-toDo:hover {
  background-color: #fff;
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.03);
}

.circle {
  width: 10px;
  height: 10px;
  background: #64c4ed;
  border-radius: 50%;
}

.circle1 {
  width: 10px;
  height: 10px;
  background: #42b883;
  border-radius: 50%;
}

.circle2 {
  width: 10px;
  height: 10px;
  background: #ffbbcc;
  border-radius: 50%;
}
.circle3 {
  width: 10px;
  height: 10px;
  background: #b6e6bd;
  border-radius: 50%;
}
.circle4 {
  width: 10px;
  height: 10px;
  background: #c9d1d3;
  border-radius: 50%;
}

.cancel {
  color: #e5e5e5;
}

.button-cancel {
  background: none;
  border: none;
  margin-top: 2px;
}
.button-cancel img {
  width: 15px;
}

.sideleft {
  display: flex;
  align-items: center;
  gap: 10px;
}

.add-list {
  margin-top: 48px;
  margin-left: 7px;
  display: flex;
  gap: 10px;
  align-items: center;
  position: relative;
}
.sidebar__plus {
  color: #868686;
  font-size: 30px;
}
.sidebar-text-add {
  margin-top: 4px;
}

.sidebar-modal {
  /* width: 235px; */
  background-color: #fff;
  position: absolute;
  top: 45px;
  box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.05);
  border-radius: 10px;
  padding: 0px 15px 15px 20px;
}
.sidebar-modal input {
  width: 200px;
  height: 32px;
  background: #ffffff;
  border: 1px solid #efefef;
  border-radius: 4px;
  outline: none;
}

input::placeholder {
  padding-left: 11px;
}

.circle_change {
  display: flex;
  margin-top: 15px;
  gap: 5px;
}
.child-circle {
  width: 20px;
  height: 20px;
  background-color: #42b883;
  border-radius: 50%;
}
.addbutton {
  background: #4dd599;
  border-radius: 4px;
  padding: 10px 70px;
  color: #fff;
  margin-top: 15px;

  border: none;
  cursor: pointer;
}

.child-circle:nth-child(1) {
  background-color: #c9d1d3;
}
.child-circle:nth-child(2) {
  background-color: #42b883;
}
.child-circle:nth-child(3) {
  background-color: #64c4ed;
}
.child-circle:nth-child(4) {
  background-color: #ffbbcc;
}
.child-circle:nth-child(5) {
  background-color: #b6e6bd;
}
.child-circle:nth-child(6) {
  background-color: #c355f5;
}
.child-circle:nth-child(7) {
  background-color: #09011a;
}
.child-circle:nth-child(8) {
  background-color: #ff6464;
}

.model-cancel {
  background: #5c5c5c;
  width: 20px;
  height: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  float: right;
  position: relative;
  left: 1.3rem;
  color: #fff;
  border-radius: 50%;
  top: -5px;
  border: none;
  cursor: pointer;
}

.plusbutton {
  border: none;
  background: none;
  cursor: pointer;
}
</style>