<template>
    <div>
        <ul>
            <TodoItem 
                v-for="todo of todos"
                v-bind:todo="todo"
                :key="todo.id"
            />
        </ul>
    </div>
</template>

<script>
    import TodoItem from '@/components/TodoItem' 
    export default {
        props: ['todos'],
        components: {
            TodoItem
        }
    }
</script>