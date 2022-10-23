<template>
    <DeleteModal v-show="deleteModal" :type="'item'" data-cy="todo-modal-delete"/>
    <div class="todos">
        <Todo v-for="todo in todos" :key="todo.id" :todo="todo"/>  
    </div>
</template>

<script>
import { mapState } from 'vuex';
import Todo from './Todo.vue';
import DeleteModal from './DeleteModal.vue';

export default {
    components : {
        Todo,
        DeleteModal
    },
    computed : mapState(['todos', 'deleteModal'])
}
</script>

<style scoped>
    .todos {
        grid-template-columns: repeat(1, minmax(0, 1fr));
        gap: 1rem;
        display: grid;
    }
</style>