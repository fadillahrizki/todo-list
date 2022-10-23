<template>
    <DeleteModal v-show="deleteModal" :type="'activity'" data-cy="activity-modal-delete" />
    <div class="activities">
        <Activity v-for="activity in activities" :key="activity.id" :activity="activity"/>  
    </div>
</template>

<script>
import Activity from './Activity.vue';
import {mapState} from 'vuex';
import DeleteModal from './DeleteModal.vue';

export default {
    components : {
    Activity,
    DeleteModal
},
    computed: mapState(['activities', 'deleteModal']),
}
</script>

<style scoped>
    .activities {
        grid-template-columns: repeat(4, minmax(0, 1fr));
        gap: 1rem;
        display: grid;
    }
</style>