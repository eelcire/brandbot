<template>
    <header class="container">
        <button class="inputButton" @click="markAllDone">
            {{ '\u2713' }}
        </button>
        <input
            class="inputText"
            v-on:keyup="addItem"
            type="text"
            name="input"
            v-model="input"
            id="input"
            placeholder="What needs to be done?"
        />
    </header>
</template>

<script>
    export default {
        name: "Input",
        data: function() {
            return {
                input: '',
            }
        },
        methods: {
            addItem(e) {
                if (e.keyCode === 13) {
                    if (this.input === '') {
                        return
                    }
                    this.$emit('addItem', this.input)
                    this.input = ''
                }
            },
            markAllDone() {
                this.$emit('markAllDone')
            }
        }
    }
</script>

<style scoped>
    .container {
        display: flex
    }
    .inputButton {
        height: 50px;
        width: 50px;
        border: none;
        outline: none;
        cursor: pointer;
        font-size: 18px;
    }
    .inputText {
        flex: 1;
        height: 50px;
        outline: none;
        border: none;
        padding: 0;
        color: #555555;
        font-size: 18px;
    }
    ::placeholder {
        color: #e4e4e4;
    }
</style>