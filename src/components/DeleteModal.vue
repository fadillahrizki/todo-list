<template>
    <div class="modal-overlay" @click.self="toggleDeleteModal">
        <div class="modal">
            <div class="modal-body">
                <IconAlert />
                <p class="text">Apakah anda yakin menghapus {{type}} <strong data-cy="modal-delete-title">"{{selectedDelete.title}}"?</strong></p>
                <div class="buttons">
                    <Button data-cy="modal-delete-cancel-button" :type="'secondary'" @click="toggleDeleteModal">Batal</Button>
                    <Button data-cy="modal-delete-confirm-button" :type="'danger'" @click="deleteItem">Hapus</Button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import IconClose from "./icons/IconClose.vue";
import Button from "./Button.vue";
import { mapActions, mapState } from 'vuex';
import PriorityVue from "./Priority.vue";
import IconAlert from "./icons/IconAlert.vue";
export default {
    props:['type'],
    components: { IconClose, Button, PriorityVue, IconAlert },
    computed:{
        ...mapState(['selectedDelete'])
    },
    methods: {
        ...mapActions(['toggleDeleteModal', 'removeActivity', 'removeTodo', 'toggleAlert']),
        deleteItem() {
            if(this.type == 'activity') {
                this.removeActivity(this.selectedDelete.id)
            } else {
                this.removeTodo(this.selectedDelete.id)
            }

            this.toggleDeleteModal()

            this.toggleAlert()
        }
    }
}
</script>

<style scoped>
    .modal-body{
        text-align: center;
        padding:2rem;
        display: flex;
        flex-direction: column;
        gap:2rem;
        align-items: center;
        justify-content: center;
    }

    .modal{
        width:500px;
    }

    .buttons{
        display: flex;
        justify-content: center;
        gap: 2rem;
    }
</style>