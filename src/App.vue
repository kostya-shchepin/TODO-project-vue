<template>
    <div class="block">
        <h2>Список дел</h2>
        <TodoList v-if="todos.length" v-bind:todos="todos" @remove-todo="removeTodo" />
        <p class="empty" v-else>Список дел пуст</p>
        <AddTodo @add-todo="addTodo" />
    </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import AddTodo from "@/components/AddTodo.vue";
export default {
    name: "app",
    data() {
        return {
            todos: [],
        };
    },
    mounted() {
        this.todos = JSON.parse(localStorage.getItem("tasks")) || [];
    },
    watch: {
        todos: {
            handler(newTodos) {
                localStorage.setItem("tasks", JSON.stringify(newTodos));
            },
            deep: true,
        },
    },
    methods: {
        removeTodo(id) {
            this.todos = this.todos.filter((t) => t.id !== id);
            localStorage.setItem("tasks", JSON.stringify(this.todos));
        },
        addTodo(todo) {
            this.todos.push(todo);
            localStorage.setItem("tasks", JSON.stringify(this.todos));
        },
    },
    components: {
        TodoList,
        AddTodo,
    },
};
</script>

<style>
body {
    font-family: "Open Sans", sans-serif;
    font-weight: 400;
    /* background: repeat; */
    background: url("assets/tasks.png") center, linear-gradient(45deg, rgb(255, 236, 141), rgb(42, 232, 238)) fixed;
    background-repeat: space;
    height: 100%;
}

button {
    cursor: pointer;
    transition: 0.5s all;
    &:hover {
        opacity: 0.8;
    }
}

.block {
    padding: 40px;
    max-width: 500px;
    width: 100%;
    margin: 100px auto 100px;
    display: block;
    background-color: #fff;
    border-radius: 30px;
    box-shadow: 4px 15px 31px 2px rgba(120, 129, 135, 0.3);
    h2 {
        margin: 0;
        margin-bottom: 40px;
        padding: 5px;
        font-size: 36px;
        font-weight: 600;
        color: #000;
        text-align: center;
        background: #f9f9f9;
        border-radius: 15px;
    }
    .empty {
        font-size: 18px;
    }
}

.add-task {
    margin-top: 40px;
    width: 140px;
    height: 45px;
    background-color: #2fbf55;
    border: 0;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    &::after {
        content: "";
        width: 25px;
        height: 3px;
        background-color: #fff;
        position: absolute;
    }
    &::before {
        content: "";
        width: 3px;
        height: 25px;
        background-color: #fff;
        position: absolute;
    }
}
@media (max-width: 768px) {
    .block {
        padding: 30px 25px;
        margin-top: 20px;
        max-width: 80%;
        h2 {
            font-size: 28px;
            margin-bottom: 30px;
        }
        .empty {
            font-size: 16px;
        }
    }
    .add-task {
        width: 100px;
        height: 35px;
        &::before {
            width: 2px;
            height: 20px;
        }
        &::after {
            width: 20px;
            height: 2px;
        }
    }
}
</style>
