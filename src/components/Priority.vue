<template>
    <div :class="priority" data-cy="todo-item-priority-indicator"></div>
</template>

<script>
    export default {
        props:['priority']
    }
</script>

<style scoped>
    [data-cy="todo-item-priority-indicator"] {
        height: 14px;
        width: 14px;
        border-radius: 50%;
    }
</style>