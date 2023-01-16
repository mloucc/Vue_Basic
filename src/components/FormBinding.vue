<script>
import { ref } from "vue";
// const text = ref("");
// const awesome = ref(true);
let id = 0;
export default {
  data() {
    return {
      id: 0,
      myText: "Type Me show Below",
      awesome: true,
      newTodo: "",
      hideCompleted: false,
      todos: [
        { id: id++, text: "Learn HTML" },
        { id: id++, text: "Learn JavaScript" },
        { id: id++, text: "Learn Vue" },
      ],
    };
  },

  computed: {
    filteredTodos() {
      return this.hideCompleted ? this.todos.filter((t) => !t.done) : this.todos;
    },
  },

  methods: {
    toggle() {
      this.awesome = !this.awesome;
      console.log("toggle");
    },
    addTodo() {
      this.todos.push({ id: this.id++, text: this.newTodo });
      this.newTodo = "";
      console.log("add");
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
      console.log("remove");
    },
  },
};
</script>

<template>

  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta charset="utf-8" />
  </head>
  <main>

    <body>
      <!-- ----- binding text---------------- -->
      <h1>Binding Text</h1>
      <h3>
        <input v-model="myText" placeholder="Type here" />
      </h3>
      <p>
        {{ myText }}
      </p>

      <!---------- if else  ---------------------->
      <h1>If then Else</h1>
      <button @click="toggle">toggle</button>
      <h3 v-if="awesome">Vue is awesome!</h3>
      <h3 v-else>Oh no 😢</h3>

      <!-- --------- to do list --------------->
      <h1>For (to do list)</h1>
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" />
        <button>Add Todo</button>
      </form>
      <ul>
        <li v-for="todo in filteredTodos" :key="todo.id">
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
          <button @click="removeTodo(todo)">X</button>
        </li>
      </ul>
      <button @click="hideCompleted = !hideCompleted">
        {{ hideCompleted? "Show all": "Hide completed" }}
      </button>
    </body>
  </main>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
