<script setup>
import { ref } from "vue";
let id = 0;

const newTodo = ref("");
const todos = ref([
    { id: id++, text: "Learn HTML" },
    { id: id++, text: "Learn JavaScript" },
    { id: id++, text: "Learn Vue" },
]);

function addTodo() {
    todos.value.push({ id: id++, text: newTodo.value });
    newTodo.value = "";
}

function removeTodo(todo) {
    todos.value = todos.value.filter((t) => t !== todo);
}
</script>

<template>

    <head>
        <meta name="viewport" content="width=device-width， initial-scale=1.0" />
        <meta charset="utf-8" />
    </head>
    <main>

        <body>
            <form @submit.prevent="addTodo">
                div <input v-model="newTodo" />
                <button>Add Todo</button>
            </form>
        </body>
    </main>
</template>
