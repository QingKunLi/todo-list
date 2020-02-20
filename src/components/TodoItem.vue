<template>
    <div class="todo-item">
        <div :class="task.completed ? 'completed active': 'completed'" @click="complete">
            <svg class="icon">
                <use xlink:href="#right"></use>
            </svg>
        </div>
        <span>{{task.content}}</span>
        <button class="remove" @click="remove"></button>
    </div>
</template>

<script>
    import right from '../assets/images/right.svg'

    export default {
        name: "TodoItem",
        props: {
            task: {
                type: Object,
                required: true
            }
        },
        data() {
            return {
            }
        },
        methods: {
            complete() {
                this.$emit('completed', this.task)
            },
            remove() {
                this.$emit('remove', this.task)
            }
        }
    }
</script>

<style lang="scss" scoped>
    .todo-item {
        font-size: 14px;
        font-weight: 500;
        color: #303133;
        padding: 8px 4px;
        margin-top: 16px;
        border-bottom: 1px solid #dddddd;
        display: flex;
        align-items: center;

        .completed {
            margin-right: 8px;
            cursor: pointer;
            border: 1px solid transparent;

            .icon {
                width: 24px;
                height: 24px;
                vertical-align: top;
                opacity: 0;
            }
            &:hover {
                border: 1px solid #dddddd;
                border-radius: 50%;
            }

            &.active {
                .icon {
                    opacity: 1;
                }
            }
        }

        .remove {
            margin-left: auto;
            width: 24px;
            height: 24px;
            position: relative;
            background: red;
            border-radius: 50%;
            outline: none;
            border: none;
            cursor: pointer;

            &::before, &::after {
                content: '';
                display: block;
                position: absolute;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%) rotate(-45deg);
                width: 8px;
                height: 2px;
                background: #ffffff;
            }

            &::before {
            }

            &::after {
                transform: translate(-50%, -50%) rotate(45deg);
            }

        }
    }
</style>