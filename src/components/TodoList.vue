<template>
  <div class="todo__list">
    <el-card class="el-card">
      <input
        class="listt"
        type="text"
        v-model="inputval"
        @keyup="CoomentPush"
      />
      <todo-item
        v-for="todo in FilteredTodos"
        :key="todo.id"
        :todo="todo"
        @xodisa="checkfun(todo.id)"
        @toinput="inp(todo.id)"
        @edit="(newContent) => editTodo(todo.id, newContent)"
      />
      <div>
        {{ items }}
      </div>
      <div class="filter">
        <div class="filter__item" :class="{ active: filter === 'ALL' }">
          <input
            type="radio"
            name="a"
            v-model="filter"
            value="ALL"
            id="ALL"
            class="filter__input"
          />
          <label for="ALL">All</label>
        </div>
        <div class="filter__item" :class="{ active: filter === 'ACTIVE' }">
          <input
            type="radio"
            name="a"
            v-model="filter"
            value="ACTIVE"
            id="ACTIVE"
            class="filter__input"
          />
          <label for="ACTIVE">Active</label>
        </div>
        <div class="filter__item" :class="{ active: filter === 'COMPLETED' }">
          <input
            type="radio"
            name="a"
            v-model="filter"
            value="COMPLETED"
            id="COMPLETED"
            class="filter__input"
          />
          <label for="COMPLETED">Completed</label>
        </div>
      </div>
      <el-button type="primary" @click="clearcom">clear completed</el-button>
    </el-card>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "App",
  components: {
    TodoItem,
  },
  data() {
    return {
      filter: "ALL",
      inputval: "",
      todos: [
        { id: 1, content: "dars tayyorlash", completed: true },
        { id: 2, content: "ovqatlanish", completed: true },
      ],
    };
  },
  computed: {
    items() {
      const count = this.todos.filter((tod) => !tod.completed).length;
      if (count === 1) {
        return "1 item left";
      }
      return `${count} items left`;
    },
    FilteredTodos() {
      if (this.filter === "ALL") {
        return this.todos;
      }
      return this.todos.filter((tod) =>
        this.filter === "COMPLETED" ? tod.completed : !tod.completed
      );
    },
  },
  methods: {
    CoomentPush(event) {
      if (event.key === "Enter") {
        this.todos.push({
          id: this.todos.length + 1,
          content: this.inputval,
          completed: false,
        });
      }
    },
    clearcom() {
      this.todos = this.todos.filter((todo) => !todo.completed);
    },
    checkfun(todoItem) {
      this.todos = this.todos.map((todo) => {
        if (todo.id === todoItem) {
          return { ...todo, completed: !todo.completed };
        }

        return todo;
      });
    },
    inp(interr) {
      let sal = document.querySelectorAll(".sal");
      alert("salss");
      console.log(sal[interr - 1]);
      ("<input type>");
    },
    editTodo(todoId, todContent) {
      this.todos = this.todos.map((todo) => {
        if (todo.id === todoId) {
          return { ...todo, content: todContent };
        }
        return todo;
      });
    },
  },
};
</script>

<style lang="scss">
.todo__list {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  .listt {
    height: 55px;
    width: 100%;
    border: 1px solid blue;
    font-size: 18px;
    border-radius: 7px;
    padding: 15px;
  }
}
.el-card {
  width: 70%;
}
.filter {
  display: flex;
  margin: 10px 0;
  .filter__item {
    display: flex;
    align-items: center;
  }
  .active {
    border: 1px solid;
    border-radius: 5px;
    //  background-color: #409eff;
    border-color: #409eff;
  }
  .filter__input {
    display: none;
  }
  label {
    cursor: pointer;
    padding: 5px 10px;
  }
}
</style>
