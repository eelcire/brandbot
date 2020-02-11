<template>
    <section class="container">
        <div class="todo" v-for="(todo) in todos" v-bind:key="todo.id">
            <button class="inputButton" v-bind:class="todo.done ? 'active' : null" v-on:click="() => markDone(todo.id)">
                {{ '\u2713' }}
            </button>
            <label :style="{'z-index': index}" @dblclick="toggleDisable(todo.id)" for="inputText"></label>
            <input
                :id="todo.id"
                :disabled="active"
                class="inputText"
                v-bind:class="[todo.done ? 'activeText' : null]"
                v-on:keyup="editTodo"
                v-model="todo.name">
            <button class="remove" v-on:click="() => removeTodo(todo.id)">
                X
            </button>
        </div>
    </section>
</template>

<script>
    export default {
        name: 'Todos',
        props: ['todos'],
        data: function() {
            return {
                active: true,
                todo: '',
                index: 1,
                clicked: null,
            }
        },
        methods: {
            removeTodo(id) {
                this.$emit('removeTodo', id)
            },
            markDone(id) {
                this.$emit('markDone', id)
            },
            editTodo(e) {
                if (e.keyCode === 13) {
                    if (e.target.value === '') {
                        return
                    }
                    this.$emit('saveTodos')
                    this.toggleDisable(e.target.value)
                } else if (e.keyCode === 27) {
                    this.toggleDisable(e.target.value)
                    e.target.value = this.todo
                }
            },
            toggleDisable(id) {
                this.clicked = id
                this.active = !this.active
                if (this.index === 1) {
                    this.index = -1
                } else {
                    this.index = 1
                }
                for (let todo of this.todos) {
                    if (todo.id === id)
                    this.todo = todo.name
                }
            }
        }
    }
</script>

<style scoped>
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: white;
    }
    .todo {
        width: 100%;
        display: flex;
        border-top: 1px solid #e6e6e6;
    }
    .inputText {
        flex: 1;
        outline: none;
        border: none;
        padding: 0;
        text-indent: 5px;
        font-size: 18px;
        transition: color 0.4s;
        color: rgb(59, 59, 59);
        font-weight: 200;
    }
    .inputButton {
        height: 50px;
        width: 50px;
        outline: none;
        border: none;
        font-size: 18px;
    }
    .remove {
        outline: none;
        border: none;
        font-size: 18px;
        color: rgb(185, 113, 113);
        visibility: hidden;
        align-items: center;
        transition: color 0.2 ease-out;
        z-index: 2
    }
    .active {
        background-color: #a0a0a0;
        border-radius: 25px;
    }
    .activeText {
        text-decoration: line-through;
        color: #7e7e7e;
    }
    .todo:hover .remove {
        visibility: visible;
    }
    .remove:hover {
        color:rgb(187, 146, 146)
    }
    label {
        flex: none;
        position: absolute;
        height: 50px;
        width: 100%;
        margin-left: 50px;
    }
    .editText {
        color: red;
    }
</style>