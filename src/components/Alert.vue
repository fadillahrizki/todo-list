<template>
    <div class="modal-overlay" @click.self="toggleAlert">
        <div class="modal" data-cy="modal-information">
            <div class="modal-body">
                <IconInfo data-cy="modal-information-icon" /> 
                <span data-cy="modal-information-title">{{message}}</span>
            </div>
        </div>
    </div>
</template>

<script>
import { mapActions } from 'vuex';
import IconInfo from "./icons/IconInfo.vue";
export default {
    props:['message'],
    components: { IconInfo },
    methods:{
        ...mapActions(['toggleAlert'])
    }
}
</script>

<style scoped>
    .modal-body {
        display: flex;
        align-items: center;
        gap:1rem;
        font-weight: 500;
    }
    .modal {
        width: 500px;
    }
</style>