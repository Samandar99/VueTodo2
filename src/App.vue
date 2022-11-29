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

      <div class="container-checkbox" v-for="todos in todoApp" :key="todos.id">
        <input class="input" type="checkbox" id="check" />
        <label class="texttask">{{ todos.name }}</label>
        <button @click="delUser(todos.id)">
          <i class="fa fa-times fa-lg can"></i>
        </button>
      </div>

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
      todoApp: [{ id: idApp++, name: "" }],
    };
  },
  watch: {
    // text(newValue){
    //   console.log(newValue);
    // }
    todoApp: {
      handler(updatedUsersnew) {
        localStorage.setItem("lists", JSON.stringify(this.todoApp));
      },
      deep: true,
    },
  },

  created() {
    this.getTodoList();
  },

  methods: {
    addText() {
      if (this.text === "") {
        return;
      }

      this.todoApp.push({
        id: idApp++,
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
    delUser(id) {
      let index = this.todoApp.findIndex((user) => user.id === id);
      this.todoApp.splice(index, 1);
    },
    getTodoList() {
      let locaList = localStorage.getItem("lists");
      if (locaList) {
        this.todoApp = JSON.parse(locaList);
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
  max-width: 800px;
  height: 500px;
  margin-top: 47px;
  /* background-color: rebeccapurple; */
  flex: 1;
}
.conatiner-app h1 {
  color: #64c4ed;
  font-weight: 900;
  font-size: 42px;
  font-family: "Montserrat";
}

.container-checkbox {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}
.container-checkbox button {
  background: none;
  border: none;
  cursor: pointer;
}

.input[type="checkbox"] {
  appearance: none;
  -webkit-appearance: none;
  height: 25px;
  width: 25px;

  border: 1px solid #d5d5d5;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}
.input[type="checkbox"]:after {
  font-family: "Font Awesome 5 Free";
  font-weight: 900;
  content: "\f00c";
  font-size: 17px;
  color: #fff;
  display: none;
}
/* .input[type="checkbox"]:hover {
  background-color: #a5a5a5;
} */
.input[type="checkbox"]:checked {
  background-color: #5dcd3e;
}

.input[type="checkbox"]:checked:after {
  display: block;
}
.texttask {
  margin-left: 15px;
}
.can {
  margin-left: 20px;
  color: #e3e3e3;
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
  max-width: 420px;
  margin-top: 30px;
  margin-bottom: 41px;
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


