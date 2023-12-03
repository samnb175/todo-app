<template>
    <div class="tasks-wrapper">
        <ul class="list-group mt-4">
            <li v-for="task in taskList" class="task list-group-item d-flex column-gap-3 justify-content-between" :class="{'completed':task.isComplete}">
                <div class="title">
                    <label class="container">
                        <input type="checkbox" v-model="task.isComplete">
                        <span class="checkmark"><i class="bi bi-check-lg"></i></span>
                        <span class="mx-2">{{ task.name }}</span>
                    </label>
                </div>
                <div class="actions">
                    <span @click="handleCurrentTask($event, task, 'edit')" class="mx-4"><i class="bi bi-pencil-square"></i></span>
                    <span @click="handleCurrentTask($event, task, 'delete')"><i class="bi bi-trash3"></i></span>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'Tasks',
        props: ['taskList'],
        methods: {
            handleCurrentTask(e, currTask, eventName) {
                this.$emit(eventName, {task: currTask})
            }
        }
    }
</script>

<style>
    .task.completed {
        color: #bbbbbb;
        background-color: #ebfdec;
    }

    .task.completed .title label {
        cursor: pointer;
        text-decoration: line-through;
    }

    .container {
        display: block;
        position: relative;
        padding-left: 1.5rem;
        cursor: pointer;
        font-size: 1rem;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }

    .container input {
        position: absolute;
        opacity: 0;
        cursor: pointer;
        height: 0;
        width: 0;
    }

    .checkmark {
        position: absolute;
        top: 0;
        left: 0;
        height: 20px;
        width: 20px;
        border-radius: 3px;
        border: 1px solid #93B1A6;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .container input:checked ~ .checkmark {
        border-color: #93B1A6;
    }

    .checkmark i {
        display: none;
        position: absolute;
        color: #45FFCA;
        transform: scale(2) rotate(360deg) translate(2px, -1px)
    }

    .container input:checked ~ .checkmark i {
        display: block;
    }

</style>