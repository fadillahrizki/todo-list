<template>
    <div class="modal-overlay" @click.self="toggleModal">
        <div class="modal">
            <div class="modal-header">
                <h3>Tambah List Item</h3>
                <IconClose data-cy="modal-add-close-button" @click="toggleModal" />
            </div>
            <div class="modal-body">
                <div class="form-group">
                    <label for="">Nama List Item</label>
                    <input type="text" placeholder="Tambahkan nama item" v-model="title">
                </div>
                <div class="form-group">
                    <label for="">Priority</label>
                    <v-select id="priority" :options="options" v-model="priority" :reduce="option => option.value" label="title">
                        <template v-slot:option="option">
                            <div class="flex">
                                <PriorityVue :priority="option.value" />
                                <span>{{ option.title }}</span>
                            </div>
                        </template>
                        <template v-slot:selected-option="option">
                            <div class="flex">
                                <PriorityVue :priority="option.value" />
                                <span>{{ option.title }}</span>
                            </div>
                        </template>
                    </v-select>
                </div>
            </div>
            <div class="modal-footer">
                <div></div>
                <Button @click="saveItem" :type="'primary'" data-cy="modal-add-save-button" :disabled="!title">Simpan</Button>
            </div>
        </div>
    </div>
</template>

<script>
import IconClose from "./icons/IconClose.vue";
import Button from "./Button.vue";
import { mapActions, mapState } from 'vuex';
import PriorityVue from "./Priority.vue";
export default {
    components: { IconClose, Button, PriorityVue },
    data : () => ({
        title: '',
        priority: 'very-high',
        options: [
            {
                title: 'Very High',
                value: 'very-high'
            },
            {
                title: 'High',
                value: 'high'
            },
            {
                title: 'Medium',
                value: 'normal'
            },
            {
                title: 'Low',
                value: 'low'
            },
            {
                title: 'Very Low',
                value: 'very-low'
            },
        ]
    }),
    computed:{
        ...mapState(['selectedTodo'])
    },
    watch:{
        selectedTodo(){
            if(this.selectedTodo){
                this.title = this.selectedTodo.title
                this.priority = this.selectedTodo.priority
            }
        }
    },
    methods: {
        ...mapActions(['addTodo', 'updateTodo', 'toggleModal']),
        saveItem() {
            if(this.selectedTodo) {
                this.selectedTodo.title = this.title
                this.selectedTodo.priority = this.priority
                this.updateTodo(this.selectedTodo)
            } else {
                this.addTodo({
                    activity_group_id: this.$route.params.id,
                    title: this.title,
                    priority: this.priority
                })
            }

            this.title = ''
            this.priority = 'very-high'
        }
    }
}
</script>

<style scoped>
.form-group{
    margin:12px 0;
}

.flex {
    display: flex;
    gap: 0.5rem;
    justify-items: center;
    align-items: center;
}

.form-group label {
    display: block;
    margin-bottom: 12px;
}

.form-group input{
    width:100%;
    padding: 12px;
    border: 1px solid #dee2e6;
    border-radius: 6px;
}

[data-cy="modal-add-close-button"] {
    cursor: pointer;
}
</style>