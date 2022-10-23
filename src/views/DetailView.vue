<template>
  <main>
    <Modal v-show="showModal"/>
    <Alert v-show="showAlert"  :message="'Item berhasil dihapus'" />
    <div class="between mb">
      <div class="between">
        <IconBack @click="$router.replace({ name: 'home'})" data-cy="todo-back-button"/>
        <input v-if="edit" type="text" v-model="activity.title">
        <h1 v-else data-cy="todo-title">{{activity.title}}</h1>
        <IconPen @click="edit = !edit" data-cy="todo-title-edit-button" />
      </div>
      <div class="between sort">
        <IconSort v-show="todos.length > 0" data-cy="todo-sort-button" @click="showFilter = !showFilter"/>
        <Button data-cy="todo-add-button" type="primary" @click="toggleModal">
          <IconPlus /> <span>Tambah</span>
        </Button>

        <div class="sort-items" v-show="showFilter">
          <div data-cy="sort-selection" v-for="item in sortItems" :key="item.label" @click="selectFilter(item)"> 
            <div class="between">
                <IconSort data-cy="sort-selection-icon" :type="item.icon" /> 
                <span data-cy="sort-selection-title">{{item.label}}</span>
            </div> 
            <IconCheck v-show="item.label == selectedSort"/> 
          </div>
        </div>
      </div>
    </div>
    <TodosView v-if="todos.length > 0"/>
    <img v-else data-cy="todo-empty-state" @click="toggleModal" src="@/assets/todo-empty.png" alt="empty" />
  </main>
</template>

<script>
import { mapActions, mapMutations, mapState } from 'vuex';
import Button from '../components/Button.vue';
import IconPlus from '../components/icons/IconPlus.vue';
import TodosView from '../components/Todos.vue';
import IconBack from '../components/icons/IconBack.vue';
import IconPen from '../components/icons/IconPen.vue';
import Modal from '../components/Modal.vue';
import IconSort from '../components/icons/IconSort.vue';
import IconCheck from '../components/icons/IconCheck.vue';
import Alert from '../components/Alert.vue';

export default {
  components: {
    Button,
    IconPlus,
    TodosView,
    IconBack,
    IconPen,
    Modal,
    IconSort,
    IconCheck,
    Alert
},
  created(){
    this.findActivity(this.$route.params.id)
    this.fetchTodos(this.$route.params.id)
  },  
  computed: {
    ...mapState(['showModal', 'activity', 'todos', 'selectedSort', 'showAlert']),
  },
  data : () => ({
    edit:false,
    showFilter:false,
    sortItems: [
      {
        label:'Terbaru', 
        icon: 'IconSortNewest'
      },
      {
        label: 'Terlama',
        icon: 'IconSortOldest'
      },
      {
        label: 'A-Z',
        icon: 'IconSortAz'
      },
      {
        label: 'Z-A',
        icon: 'IconSortZa'
      },
      {
        label: 'Belum Selesai',
        icon: 'IconSortUnfinished'
      },
    ],
  }), 
  methods: {
    ...mapActions(['addTodo', 'toggleModal', 'findActivity', 'updateActivity', 'fetchTodos']),
    ...mapMutations(['sortBy']),
    selectFilter(filter){
      this.sortBy(filter.label)
      this.showFilter = false
    }
  },
  watch:{
    'activity.title'(){
      this.updateActivity(this.activity)
    }
  }
}
</script>

<style scoped>
[data-cy='todo-back-button'],[data-cy='todo-title-edit-button'] {
    cursor: pointer;
  }

  [type='text'] {
    font-size: 1.5rem;
    border:none;
    border-radius: 999px;
    padding: 12px 24px;
  }

  [data-cy="todo-sort-button"] {
    border:1px solid #e5e5e5;
    width:54px;
    height:54px;
    padding: 12px;
    border-radius: 50%;
    cursor: pointer;
  }

  .sort {
    position:relative;
  }

  .sort-items {
    background:white;
    box-shadow: 8px 4px 8px 0 rgb(0 0 0 / 10%);
    border-radius: 10px;
    overflow: hidden;
    position: absolute;
    top:120%;
  }

  .sort-items > div {
    padding:1rem;
    border-bottom: 1px solid #e5e5e5;
    display: flex;
    width:235px;
    justify-content: space-between;
    align-items: center;
    gap:0.5rem;
    cursor: pointer;
  }

  .sort-items > div:hover {
    background: #e9ecef;
  }
</style>