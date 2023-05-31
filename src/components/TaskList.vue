<script setup lang="ts">
    import { CheckIcon, XMarkIcon } from "@heroicons/vue/24/solid"

    import { ref } from "vue"

    const props = defineProps({
        tasks: Array<string>,
        done: Boolean
    })

    const emit = defineEmits(['checked'])
</script>

<template>
    <label for="tasks"><slot></slot></label>
    <ol class="space-y-4 list-decimal" id="tasks">
        <li v-for="task of tasks" v-if="!done">
            <p class="flex-grow w-fit h-fit place-self-center mt-0.5">{{task}}</p>
            <button class="p-1 bg-zinc-900 rounded-xl" @click="emit('checked', task)">
                <CheckIcon class="w-7 h-7 fill-gray-100"></CheckIcon>
            </button>
        </li>
        <li class="flex bg-zinc-700 max-w-full"
        v-for="task of tasks" v-else>
            <p class="flex-grow w-fit h-fit place-self-center mt-0.5 line-through text-gray-500">{{task}}</p>
            <button class="p-1 bg-zinc-900 rounded-xl" @click="emit('checked', task)">
                <XMarkIcon class="w-7 h-7 fill-gray-100"></XMarkIcon>
            </button>
        </li>
    </ol>
</template>

<style scoped>
    li {
        padding: 0.5rem 0.5rem 0.5rem 1rem;
        display: flex;
        background-color: rgb(63, 63, 70);
        border-radius: 0.75rem;
        margin: 1rem 0 1rem 0;
        width: 100%;
    }

    p, label {
        place-self: center;
    }

    p {
        overflow: auto;
        overflow-anchor: none;
        overflow-wrap: break-word;
    }

    ol {
        list-style-type: decimal;
        list-style-position: inside;
        padding: 0.5rem 1rem 1rem 1rem;
        width: 100%
    }

    label {
        font-weight: 700;
        text-decoration: underline;
        width: 100%;
        padding: 0.25rem;
        display: flex;
        height: 2.5rem;
        max-height: 2.5rem;
    }

    XMarkIcon, CheckIcon {
        display: flex;
        flex-flow: column;
        width: 1.75rem;
        height: 1.75rem;
        max-height: 1.75rem;
        max-width: 1.75rem;
    }
</style>