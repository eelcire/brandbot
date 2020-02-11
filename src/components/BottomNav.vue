<template>
    <section id="todos">
        <footer class = "container">
            <p class = "ptext">{{ filteredTodos.length }} items left</p>
            <div class="buttons">
                <button @click="filterAll">All</button>
                <button @click="filterActive">Active</button>
                <button @click="filterCompleted">Completed</button>
            </div>
            <button @click="clearCompleted">Clear completed</button>
        </footer>
    </section>
</template>

<script>
    export default {
        name: 'BottomNav',
        props: ['filteredTodos'],
        data: function() {
			return {
                todos: this.filteredTodos,
			}
        },
        methods: {
            filterAll() {
                this.$emit('filterAll')
            },
            filterActive() {
                this.$emit('filterActive')
            },
            filterCompleted() {
                this.$emit('filterCompleted')
            },
            clearCompleted() {
                this.$emit('clearCompleted')
            }
        }
    }
</script>

<style scoped>
    .container {
        background-color: white;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
    button {
        height: 50px;
        min-width: 50px;
        outline: none;
        border: none;
        cursor: pointer;
    }
    .ptext {
        font-size: 13px;
        font-weight: 100;
        color: rgb(131, 131, 131);
    }
    button.selected {
        border-color: rgba(175, 47, 47, 0.2)
    }
</style>