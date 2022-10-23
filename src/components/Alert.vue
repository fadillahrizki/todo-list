<template>
    <div class="modal-overlay" @click.self="toggleAlert">
        <div class="modal">
            <div class="modal-body">
                <IconInfo /> {{message}}
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