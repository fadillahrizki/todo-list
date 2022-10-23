<template>
  <main>
    <Alert v-show="showAlert" :message="'Activity berhasil dihapus'" />
    <div class="between mb">
      <h1 data-cy="activity-title">Activity</h1>
      <Button data-cy="activity-add-button" type="primary" @click="addActivity"> <IconPlus /> <span>Tambah</span> </Button>
    </div>
    <ActivitiesVue v-if="activities.length > 0"/>
    <img v-else data-cy="activity-empty-state" @click="addActivity" src="@/assets/activity-empty.png" alt="empty" />
  </main>
</template>

<script>
import Button from '../components/Button.vue';
import IconPlus from '../components/icons/IconPlus.vue';
import ActivitiesVue from '../components/Activities.vue';
import { mapActions, mapState } from 'vuex';
import DeleteModal from '../components/DeleteModal.vue';
import Alert from '../components/Alert.vue';

export default {
  components:{
    Button,
    IconPlus,
    ActivitiesVue,
    DeleteModal,
    Alert
},
  computed: mapState(['activities', 'deleteModal', 'showAlert']),
  created(){
    this.fetchActivities()
  },
  methods: {
    ...mapActions(['addActivity','fetchActivities'])
  }
}
</script>