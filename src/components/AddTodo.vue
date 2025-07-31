<template>
    <button class="add-task" @click="toggleActive"><div class="plus"></div></button>
    <div class="popup__bg" v-bind:class="{ active: isActive }">
        <div class="popup" v-bind:class="{ active: isActive }">
            <div class="close-popup" @click="toggleActive">+</div>
            <form @submit.prevent="onSubmit">
                <label>
                    <input type="text" name="name" class="task-input" v-model="title" />
                    <div class="label__text">Введите дело</div>
                </label>
                <button type="submit">Добавить</button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            title: "",
            isActive: false,
        };
    },
    methods: {
        onSubmit() {
            console.log("Submit", this.title);
            if (this.title.trim) {
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    completed: false,
                };
                this.$emit("add-todo", newTodo);
                this.title = "";
            }
            this.toggleActive();
        },
        toggleActive() {
            this.isActive = !this.isActive;
        },
    },
};
</script>

<style scoped>
.popup__bg {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, 0.5);
    opacity: 0;
    pointer-events: none;
    transition: 0.5s all;
    &.active {
        opacity: 1;
        pointer-events: all;
        transition: 0.5s all;
    }
}
.popup {
    position: absolute;
    z-index: 1;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(0);
    background: #fff;
    width: 400px;
    padding: 30px;
    transition: 0.5s all;
    border-radius: 30px;
    label {
        width: 100%;
        margin-bottom: 25px;
        display: flex;
        flex-direction: column-reverse;
    }
    .label__text {
        font-size: 21px;
        font-weight: 500;
        color: #222;
        margin-bottom: 5px;
    }
    input {
        height: 45px;
        font-size: 18px;
        border: none;
        outline: none;
        border-bottom: 1px solid #cfd0d3;
        &:focus {
            border-bottom: 1px solid#03abff;
            & + .label__text {
                color: #03abff;
            }
        }
    }
    textarea {
        resize: none;
        width: 100%;
        height: 150px;
        border: none;
        outline: none;
        border-bottom: 1px solid #cfd0d3;
        font-size: 18px;
        padding-top: 5px;
        &:focus {
            border-bottom: 1px solid #03abff;
            & + .label__text {
                color: #03abff;
            }
        }
    }
    button {
        width: 100%;
        height: 60px;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #fff;
        font-size: 24px;
        letter-spacing: 1px;
        border-radius: 10px;
        background: #2fbf55;
        cursor: pointer;
        border: 0;
    }
    &.active {
        transform: translate(-50%, -50%) scale(1);
        transition: 0.5s all;
    }
    & .close-popup {
        position: absolute;
        top: 10px;
        right: 25px;
        font-size: 42px;
        font-weight: 300;
        color: #fa4141;
        cursor: pointer;
        transform: rotate(-45deg);
    }
}
</style>
