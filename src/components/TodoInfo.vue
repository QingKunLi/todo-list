<template>
    <div class="todo-info">
        <span>{{uncompletedTaskNumber}} items left</span>
        <div class="states">
            <button @click="display('all')">all</button>
            <button @click="display('active')">active</button>
            <button @click="display('completed')">completed</button>
        </div>
        <button class="clear" @click="clear">clear completed</button>
    </div>
</template>

<script>
    export default {
        name: "TodoInfo",
        props: ['tasks'],
        computed: {
            uncompletedTaskNumber() {
                let count = 0
                this.tasks.forEach(item=>{
                    if (!item.completed) count += 1
                })
                return count
            }
        },
        methods: {
            display(type) {
                this.$emit('display', type)
            },
            clear() {
                let completedTasks = []
                this.tasks.forEach(item=>{
                    if (item.completed) completedTasks.push(item)
                })
                this.$emit('clear', completedTasks)
            }
        }
    }
</script>

<style lang="scss" scoped>
    @mixin hover {
        border: 1px solid #409eff;
        color: #409eff;
    }
    .todo-info {
        margin: 16px 0;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 12px;
        font-weight: 400;

        .states {
            button {
                font-size: inherit;
                border: none;
                outline: none;
                margin-left: 8px;
                padding: 4px;
                border: 1px solid transparent;
                border-radius: 4px;

                &:hover {
                    @include hover;
                }
            }
        }

        .clear {
            font-size: inherit;
            border: none;
            outline: none;
            padding: 4px;
            border: 1px solid transparent;
            border-radius: 4px;

            &:hover {
                @include hover;
            }
        }
    }
</style>