<template>
    <div class="navbar">
        <h2 data-cy="header-title">TO DO LIST APP</h2>
    </div>
</template>

<style scoped>
    .navbar {
        background: var(--primary-color);
        padding:2rem 12rem;
        box-shadow: 0 10px 15px -3px rgb(0 0 0 / .1),
            0 4px 6px -4px rgb(0 0 0 / .1);
        position: sticky;
        top:0;
    }
    .navbar h2 {
        font-size:1.5rem;
        line-height:2rem;
        font-weight: 700;
        color:var(--white-color);
    }
</style>