<template>
    <section id="todos">
        <header>
            <h1>Todos</h1>
        </header>
    </section>
</template>

<script>
    export default {
        name: 'Header',
        props: ['todos'],
        methods: {
            removeTodo(id) {
                this.$emit('removeTodo', id)
            },
            markDone(id) {
                this.$emit('markDone', id)
            }
        }
    }
</script>

<style scoped>

</style>