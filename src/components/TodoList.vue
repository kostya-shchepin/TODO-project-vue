<template>
    <div class="task-block">
        <TodoItem v-for="(todo, i) of todos" v-bind:todo="todo" v-bind:index="i" v-on:remove-todo="RemoveTodo" />
    </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
    props: ["todos"],
    components: {
        TodoItem,
    },
    methods: {
        RemoveTodo(id) {
            this.$emit("remove-todo", id);
        },
    },
};
</script>

<style scoped>
.task-block {
    display: flex;
    flex-direction: column;
    gap: 20px;
}
</style>
