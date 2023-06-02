<script setup lang="ts">
    import {TrashIcon, PlusIcon, CheckIcon} from "@heroicons/vue/24/solid"

    import TaskList from "./TaskList.vue"
</script>

<script lang="ts">
    export default {
        data() {
            return {
                tasks: new Array<string>(),
                currentTask: "",
                completedTasks: new Array<string>()
            }
        },
        methods: {
            addTask() {
                console.log(typeof(this.tasks))
                const task = this.currentTask.trim()
                if(task == "") {
                    return
                }
                if(this.tasks.includes(task) || this.completedTasks.includes(task)) {
                    alert("This task was already added!")
                    return
                }
                this.tasks.push(task)
                this.currentTask = ""
            },

            markCompleted(task: string) {
                this.tasks = this.tasks.filter((v) => v != task)
                this.completedTasks.push(task)
            },

            markIncomplete(task: string) {
                this.completedTasks = this.completedTasks.filter((v) => v != task)
                this.tasks.push(task)
            }
        }
    }
</script>

<template>
    <header class="flex space-x-4">
        <input v-model="currentTask" class="flex-auto shadow p-1.5 bg-zinc-900"
        placeholder="Add a new task..." >
        <button @click="addTask" class="p-1 bg-zinc-900 rounded-xl">
            <PlusIcon class="w-7 h-7"/>
        </button>
    </header>
    <main class="md:flex mt-10 space-x-2">
        <div class="flex-row w-full md:w-1/2 pr-1 mr-4">
            <TaskList @checked="(task) => markCompleted(task)" :tasks="tasks">Tasks: </TaskList>
        </div>
        <div class="flex-row w-full md:w-1/2 pr-1 mr-4">
            <TaskList @checked="(task) => markIncomplete(task)" :tasks="completedTasks" done>Completed: </TaskList>
        </div>
    </main>
</template>