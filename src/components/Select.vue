<script>
import axios from 'axios'

export default {
    data() {
        return {
            cats: [],
            cat_selected: {},
            i_new_cat: '',
            i_new_todo: '',
            b_addcat: false,
            b_delcat: false,
            b_add_todo: false,
            b_del_todo: false,
            b_hide_completed: false,
            todos: [],
            xurl: '',
            todo_done: false,
        }
    },
    methods: {
        async f_fetch_cat() {
            this.cats = null;
            const res = await fetch(`http://127.0.0.1:5000/category`);
            this.cats = await res.json();
            this.cat_selected = this.cats[0];
            this.f_fetch_todo(this.cat_selected.id)
        },
        async f_fetch_todo(id) {
            this.todos = null;
            console.log("fetch todos: id = " + id);
            this.xurl = 'http://127.0.0.1:5000/todos/' + id;
            const res = await fetch(this.xurl);
            this.todos = await res.json();
            // console.log(this.todos)
        },
        async f_add_cat() {
            await axios.post('http://127.0.0.1:5000/new_cat',
                { new_cat: this.i_new_cat })
                .catch((error) => console.log(error));
            await this.f_fetch_cat();
            this.i_new_cat = '';
            this.b_addcat = false;
        },
        async f_add_todo() {
            await axios.post('http://127.0.0.1:5000/add_todo',
                {
                    cat_id: this.cat_selected.id,
                    title: this.i_new_todo,
                })
                .catch((error) => console.log(error));
            await this.f_reload_todo();
            this.i_new_todo = '';
            this.b_add_todo = false;
        },
        async f_del_todo(todo) {
            console.log("del todo: " + todo.id);
            await axios.post('http://127.0.0.1:5000/del_todo',
                todo)
                .catch((error) => console.log(error));
            await this.f_fetch_todo(this.cat_selected.id);
            this.b_add_todo = false;
        },
        async f_del_cat() {
            await axios.post('http://127.0.0.1:5000/del_cat',
                { cat_id: this.cat_selected.id })
                .catch((error) => console.log(error));
            console.log("id:" + this.cat_selected.id);
            await this.f_fetch_cat();
            this.b_delcat = false;
        },
        async f_reload_todo() {
            const id = this.cat_selected.id;
            this.todos = null;
            console.log("refetch todos: id = " + id);
            this.xurl = 'http://127.0.0.1:5000/todos/' + id;
            const res = await fetch(this.xurl);
            this.todos = await res.json();
        },
        async f_update_done(todo) {
            todo.done = !(todo.done);
            await axios.post('http://127.0.0.1:5000/update_todo',
                {
                    todo_done: todo.done,
                    todo_id: todo.id
                })
                .catch((error) => console.log(error));
            console.log("done:" + todo.done);
            this.b_delcat = false;
        },
    },
    created() {
        this.f_fetch_cat();
    },
    computed: {

    }
}
</script>


<template>
    <!-- <p> {{ cats }}</p> -->
    <!-- <p> {{ todos }}</p> -->
    <div class="mflex">
        <!-- ----- ----- ----- ----- ----- ----- ----- ----- -----  left Category -->
        <div class="left">
            <h2> Todo Category </h2>
            <!-- ----- ----- ----- ----- combobox  -->
            <select v-model="cat_selected" @change="f_reload_todo()" class="left">
                <option v-for="cat in cats" :value="cat">
                    {{ cat.name }}
                </option>
            </select>
            <!-- ----- -----  ----- ----- add delete -->
            <button @click="b_addcat = !b_addcat"> Add Cat </button>
            <button @click="b_delcat = !b_delcat"> Del Cat </button>
            <!-- ----- ----- ----- ----- add form -->
            <div v-if="b_addcat">
                <form @submit.prevent="f_add_cat">
                    <input v-model="i_new_cat" />
                    <button>Add Cat</button>
                </form>
            </div>
            <!-- ----- ----- ----- ----- delete form -->
            <div v-if="b_delcat">
                <form @submit.prevent="f_del_cat">
                    <input v-model="cat_selected.name" />
                    <button>Del Cat</button>
                </form>
            </div>


        </div>
        <!--  ----- ----- ----- ----- ----- ----- ----- ----- ----- right todo list  -->
        <div class="right">
            <div>
                <h2> Todo List </h2>
            </div>
            <h3> {{ cat_selected.name }} </h3>
            <ul>
                <li v-for="todo in todos" :value="todo">
                    <input type="checkbox" v-if="!todo.done" @change="f_update_done(todo)" class="larger" />
                    <input type="checkbox" v-if="todo.done" checked @change="f_update_done(todo)" class="larger" />
                    <button @click="f_del_todo(todo)" class="small">X</button>
                    <span :class="{ done: todo.done }"> &nbsp {{ todo.title }} </span>
                </li>
            </ul>
            <div>
                <button @click="b_add_todo = !b_add_todo"> Add Todo </button>
            </div>
            <div v-if="b_add_todo">
                <form @submit.prevent="f_add_todo">
                    <input v-model="i_new_todo" />
                    <button>Add</button>
                </form>
            </div>

        </div>
    </div>

</template>

<style>
.mflex {
    display: flex;
}

.small {
    font-size: smaller;
}

.left {
    background-color: aliceblue;
    font-size: medium;
    display: block;
    width: 250px;
}

.right {
    display: block;
    justify-content: flex-start;
    width: 400px;
    margin-left: 50px;
    background-color: azure;
}

.done {
    text-decoration: line-through;
}
</style>
