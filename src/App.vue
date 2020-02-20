<template>
    <div id="root">
        <Header></Header>
        <todo-list></todo-list>
    </div>
</template>

<script>
    import Header from "./components/Header.vue"
    import TodoList from "./components/TodoList.vue";
    export default {
        name: "App",
        components: {
            Header,
            TodoList
        }
    }
</script>

<style lang="scss">

</style>