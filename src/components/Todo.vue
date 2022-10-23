<template>
    <div data-cy="todo-item" class="between">
        <div class="between">
            <input type="checkbox" :checked="!todo.is_active" @click="updateTodoStatus({id:todo.id, is_active:!todo.is_active})" data-cy="todo-item-checkbox">
            <Priority :priority="todo.priority" />
            <h4 data-cy="todo-item-title" :class="todo.is_active ? '' : 'finish'">{{todo.title}}</h4>
            <IconPen data-cy="todo-item-edit-button" @click="findTodo(todo)"/>
        </div>
        <div class="between">
            <button data-cy="todo-item-delete-button" @click="deleteTodo"> <IconTrash/> </button>
        </div>
    </div>
</template>

<script>
import { mapActions } from 'vuex';
import IconTrash from './icons/IconTrash.vue';
import Priority from './Priority.vue';
import IconPen from './icons/IconPen.vue';

export default {
    props: ["todo"],
    components: { IconTrash, Priority, IconPen },
    methods:{
        ...mapActions(['findTodo', 'updateTodoStatus', 'toggleDeleteModal', 'selectDelete']),
        deleteTodo() {
            this.selectDelete(this.todo)
            this.toggleDeleteModal()
        }
    },
}

</script>

<style scoped>
    .finish {
        text-decoration: line-through;
        color:#888;
    }

    [data-cy='todo-item-edit-button'] {
        cursor: pointer;
        width: 20px;
        height:20px;
    }

    [data-cy='todo-item'] {
        box-shadow: 0 4px 6px -1px rgb(0 0 0 / .1),
            0 2px 4px -2px rgb(0 0 0 / .1);
        background: var(--white-color);
        padding:1.5rem;
        border-radius: 0.5rem;
    }

    [data-cy='todo-item-checkbox'] {
        height: 24px;
        width: 24px;
    }

    [data-cy='todo-item-priority'] {
        color: rgb(107 114 128);
        font-size: .875rem;
        line-height: 1.25rem;
    }

    [data-cy='todo-item-delete-button'] {
        border:none;
        text-transform: none;
        cursor: pointer;
        background: transparent;
    }
</style>