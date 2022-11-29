<template>
  <div class="conatiner">
    <Sidebar @send="getTitle" class="sid" @send2="ges" />
    <div class="not" v-if="viewTitle">
      <h4 class="title">Задачи отсутствуют</h4>
    </div>
    <div class="conatiner-app" v-if="viewTitle2">
      <div class="title_app">
        <h1>{{ titleApp }}</h1>
        <img src="@/assets/img/Pencil.svg" alt="" />
      </div>
      <div class="line"></div>

      <label
        class="container-checkbox"
        v-for="todos in todoApp"
        :key="todos.id"
      >
        <input type="checkbox" checked="checked" />
        <span class="checkmark"></span>
        {{ todos.name }}
      </label>

      <div class="addtask">
        <button @click="pass = !pass">
          <i class="fa-solid fa-plus fa-lg"></i>
        </button>
        <span>Новая задача</span>
      </div>

      <form @submit.prevent="addText" class="formNew" v-if="pass">
        <input
          v-model="text"
          type="text"
          class="formInput item1"
          placeholder="Текст задачи"
        />
        <button class="item2">Добавить задачу</button>
        <button class="item3" @click="dell">Отмена</button>
      </form>
    </div>
  </div>
</template>

<script>
import Sidebar from "@/components/Sidebar.vue";

let idApp = 1;

export default {
  components: {
    Sidebar,
  },

  data() {
    return {
      pass: false,
      viewTitle: false,
      viewTitle2: true,
      titleApp: "Фронтенд",
      text: "",
      todoApp: [
        { id: idApp++, name: "Vue Router" },
        { id: idApp++, name: "React and Vue Learn" },
      ],
    };
  },

  methods: {
    addText() {
      if (this.text === "") {
        return;
      }

      this.todoApp.push({
        name: this.text,
      });
      this.text = "";
    },

    dell() {
      this.text = "";
    },

    getTitle(num) {
      if (num > 0) {
        this.viewTitle = false;
      } else {
        this.viewTitle = true;
      }
    },
    ges(nums) {
      if (nums > 0) {
        this.viewTitle2 = true;
      } else {
        this.viewTitle2 = false;
      }
    },
  },
};
</script>

<style scoped>
.title {
  color: #c9d1d3;
  font-weight: 700;
  font-size: 32px;
  font-family: "Montserrat";
}

.conatiner {
  display: flex;
  gap: 67px;
}

.not {
  width: 600px;
  margin: auto;
}

.not h1 {
  font-weight: bold;
  font-size: 42px;
}
.conatiner-app {
  width: 800px;
  height: 500px;

  margin-top: 47px;
}
.conatiner-app h1 {
  color: #64c4ed;
  font-weight: 900;
  font-size: 42px;
  font-family: "Montserrat";
}
.title_app {
  display: flex;
  gap: 15px;
}
.title_app img {
  margin-top: 8px;
  width: 20px;
}

.line {
  border: 1px solid silver;
  width: 420px;
  margin-top: 30px;
  margin-bottom: 41px;
}

.container-checkbox {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;

  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container-checkbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;

  border: 1px solid #e8e8e8;
  border-radius: 50%;
}

/* On mouse-over, add a grey background color */

/* When the checkbox is checked, add a blue background */
.container-checkbox input:checked ~ .checkmark {
  background-color: #4dd599;
  border-radius: 50%;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container-checkbox input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container-checkbox .checkmark:after {
  left: 7.3px;
  top: 3px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

.addtask {
  margin-top: 25px;
  margin-bottom: 1rem;
}

.addtask button {
  background: none;
  border: none;
}
.addtask button i {
  color: #b4b4b4;
  cursor: pointer;
}
.addtask span {
  margin-left: 20px;
  font-size: 19px;
  color: #b4b4b4;
}

.formInput {
  width: 415px;
  height: 38px;
  border: 1px solid #efefef;
  border-radius: 4px;
}
.formInput::placeholder {
  padding-left: 11px;
  color: #c7c7c7;
  font-size: 14px;
}

.item1 {
  display: block;
  margin-bottom: 16px;
  outline: none;
}

.item2 {
  padding: 10px 30px;
  background: #4dd599;
  border: none;
  border-radius: 4px;
  color: #fff;
  cursor: pointer;
}

.item3 {
  margin-left: 9px;
  padding: 10px 20px;
  background: #f4f6f8;
  border: none;
  border-radius: 4px;
  color: #9c9c9c;
  cursor: pointer;
}
</style>


