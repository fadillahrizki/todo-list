<template>
    <button :class="type"> <slot></slot> </button>
</template>

<script>
export default {
    props:['type']
}
</script>

<style scoped>
button {
        font-weight: 700;
        padding: 1rem 2rem;
        border-radius: 9999px;
        cursor: pointer;
        color:var(--white-color);
        border: none;
        display: flex;
        justify-content: center;
        align-items: center;
        gap:0.25rem;
    }

    button:disabled {
        opacity: 0.5;
        cursor:no-drop;
    }

    .primary {
        background: var(--primary-color);
    }

    .secondary {
        background: var(--secondary-color);
        color:#4a4a4a;
    }

    .danger {
        background: var(--red-color);
    }
</style>