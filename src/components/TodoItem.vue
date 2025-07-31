<template>
    <div class="task">
        <input type="checkbox" class="task-checkbox" v-model="todo.completed" />
        <span v-bind:class="{ done: todo.completed }">
            {{ todo.title }}
        </span>
        <button class="delete-task" v-on:click="$emit('remove-todo', todo.id)">
            <div class="minus"></div>
        </button>
    </div>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true,
        },
        index: Number,
    },
};
</script>

<style scoped>
.task {
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    font-size: 24px;
    font-weight: 500;
    span {
        transition: 100ms;
    }
    .task-checkbox {
        margin-right: 15px;
        appearance: none;
        position: relative;
        width: 40px;
        height: 40px;
        border-radius: 10px;
        border: 4px solid #03abff;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        &::after {
            content: "";
            position: absolute;
            width: 0px;
            height: 0px;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' width='42' height='34' viewBox='0 0 42 34' fill='none'%3e%3cpath d='M16.6415 34L0 16.6047L2.37736 13.4419L15.8491 22.9302L38.8302 0L42 3.16279L16.6415 34Z' fill='black'/%3e%3c/svg%3e");
            background-size: contain;
            background-repeat: no-repeat;
            transition: 100ms;
        }
        &:checked {
            & + span.done {
                text-decoration: line-through;
                color: #cfd0d3;
            }
            &::after {
                width: 30px;
                height: 24px;
                text-decoration: line-through;
            }
        }
    }
    .delete-task {
        margin-left: 30px;
        width: 40px;
        height: 40px;
        background-color: #fa4141;
        border: 0;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        &::before {
            content: "";
            width: 25px;
            height: 3px;
            background-color: #fff;
            position: absolute;
        }
    }
}
</style>
