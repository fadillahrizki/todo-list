<template>
  <main>
    <Modal v-show="showModal"/>
    <Alert v-show="showAlert"  :message="'Item berhasil dihapus'" />
    <div class="between mb">
      <div class="between">
        <IconBack @click="$router.replace({ name: 'home'})" data-cy="todo-back-button"/>
        <h1 v-if="!edit" @click="editTitle" data-cy="todo-title">{{activity.title}}</h1>
        <input v-show="edit" type="text" class="" v-model="activity.title" @blur="updateTitle(activity.title);edit = !edit" ref="todoTitleInput" data-cy="todo-title">
        <IconPen @click="editTitle" data-cy="todo-title-edit-button" />
      </div>
      <div class="between sort">
        <IconSort v-show="todos.length > 0" data-cy="todo-sort-button" @click="showFilter = !showFilter"/>
        <Button data-cy="todo-add-button" type="primary" @click="toggleModal">
          <IconPlus /> <span>Tambah</span>
        </Button>

        <div class="sort-items" v-show="showFilter">
          <div v-for="item in sortItems" :key="item.label" @click="selectFilter(item)" data-cy="sort-selection"> 
            <div class="between" :data-cy="item.label == selectedSort ? 'sort-selection-selected' : ''">
                <IconSort :data-cy="'sort-selection-icon'" :type="item.icon" /> 
                <span :data-cy="'sort-selection-title'">{{item.label}}</span>
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
        icon: 'IconSortNewest',
        cy: 'sort-latest'
      },
      {
        label: 'Terlama',
        icon: 'IconSortOldest',
        cy: 'sort-oldest'
      },
      {
        label: 'A-Z',
        icon: 'IconSortAz',
        cy: 'sort-az'
      },
      {
        label: 'Z-A',
        icon: 'IconSortZa',
        cy: 'sort-za'
      },
      {
        label: 'Belum Selesai',
        icon: 'IconSortUnfinished',
        cy: 'sort-unfinished'
      },
    ],
  }), 
  methods: {
    ...mapActions(['addTodo', 'toggleModal', 'findActivity', 'updateTitle', 'fetchTodos']),
    ...mapMutations(['sortBy']),
    selectFilter(filter){
      this.sortBy(filter.label)
      this.showFilter = false
    },
    editTitle(){
      this.edit = !this.edit
      this.$nextTick(() => {
        this.$refs.todoTitleInput.focus();
      });
    }
  }
}
</script>

<style scoped>
[data-cy='todo-back-button'],[data-cy='todo-title-edit-button'] {
    cursor: pointer;
  }

  [data-cy="todo-title"] {
    font-size: 36px;
  }

  [type='text'] {
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