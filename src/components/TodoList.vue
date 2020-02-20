<template>
    <div class="todo-list">
        <div class="add">
            <input type="text" placeholder="I'm gonna do..." autofocus="autofocus" v-model="task" @keypress.enter="addTask">
            <button @click="addTask">
                <svg class="icon">
                    <use xlink:href="#add"></use>
                </svg>
            </button>
        </div>
        <todo-item v-for="(task, index) in displayTaskList" :key="index" :task="task" @remove="removeTask" @completed="completeTask" />
        <todo-info :tasks="taskList" @display="displayTask" @clear="clearCompletedTask"/>
    </div>
</template>

<script>
    import add from '../assets/images/add.svg'
    import TodoItem from "./TodoItem.vue";
    import TodoInfo from "./TodoInfo.vue";

    export default {
        name: "TodoList",
        components: {
            TodoItem,
            TodoInfo
        },
        data() {
            return {
                task: '',
                taskList: [],
                taskStates: 'all'
            }
        },
        methods: {
            addTask() {
                let task = {}
                task.content = this.task.trim()
                task.completed = false
                this.taskList.push(task)
                this.task = ''
            },
            removeTask(item) {
                let index = this.taskList.indexOf(item)
                this.taskList.splice(index, 1)
            },
            completeTask(item) {
                let index = this.taskList.indexOf(item)
                this.taskList[index].completed = true
            },
            displayTask(type) {
                this.taskStates = type
            },
            clearCompletedTask(completedTask) {
                this.taskList = this.taskList.filter(item=>completedTask.indexOf(item) === -1)
            }
        },
        computed: {
          displayTaskList() {
              switch (this.taskStates) {
                  case 'active':
                      return this.taskList.filter(item=>item.completed === false)
                  case 'completed':
                      return this.taskList.filter(item=>item.completed === true)
                  default:
                      return this.taskList
              }
          }
        },
        mounted() {
            this.taskList = JSON.parse(localStorage.getItem('tasks')) || []
        },
        beforeDestroy() {
            localStorage.setItem('tasks', JSON.stringify(this.taskList))
        }
    }

</script>

<style lang="scss" scoped>
    .todo-list {
        width: 62.5%;
        margin: 16px auto;
    }

    .add {
        width: 100%;
        height: 40px;
        display: flex;

        input {
            width: 100%;
            height: 100%;
            padding: 8px 16px;
            font-size: 14px;
            font-weight: 400;
            outline: none;
            border: 1px solid #dddddd;
        }

        button {
            background: #dddddd;
            outline: none;
            border: none;
            padding: 6px 12px;
            height: 100%;

            .icon {
                width: 12px;
                height: 12px;
            }
        }
    }
</style>