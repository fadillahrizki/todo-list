<template>
    <div data-cy="activity-item">
        <h4 data-cy="activity-item-title" @click="$router.replace({ name: 'detail', params: { id: activity.id } })">{{activity.title}}</h4>
        <div class="between">
            <p data-cy="activity-item-date">{{formattedDate}}</p>
            <button data-cy="activity-item-delete-button" @click="deleteActivity"> <IconTrash/> </button>
        </div>
    </div>
</template>

<script>
import { mapActions } from 'vuex';
import IconTrash from './icons/IconTrash.vue';
export default {
    props: ["activity"],
    components: { IconTrash },
    computed:{
        formattedDate(){
            return new Date(this.activity.created_at).toLocaleDateString("id-ID", { year: 'numeric', month: 'long', day: 'numeric' })
        }
    }, 
    methods:{
        ...mapActions(['removeActivity', 'toggleDeleteModal', 'selectDelete']),
        deleteActivity(){
            this.selectDelete(this.activity)
            this.toggleDeleteModal()
        }
    }
}
</script>

<style scoped>
    [data-cy='activity-item'] {
        box-shadow: 0 4px 6px -1px rgb(0 0 0 / .1),
            0 2px 4px -2px rgb(0 0 0 / .1);
        background: var(--white-color);
        padding:1.5rem;
        border-radius: 0.5rem;
        display: flex;
        flex-direction: column;
        height: 14rem;
    }

    [data-cy='activity-item-date'] {
        color: rgb(107 114 128);
        font-size: .875rem;
        line-height: 1.25rem;
    }

    [data-cy='activity-item-title'] {
        flex-grow: 2;
        cursor:pointer;
    }

    [data-cy='activity-item-delete-button'] {
        border:none;
        text-transform: none;
        cursor: pointer;
        background: transparent;
    }
</style>