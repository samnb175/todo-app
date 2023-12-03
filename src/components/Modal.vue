<template>
    <div class="modal-container w-100 h-100 position-absolute top-0 start-0 d-flex justify-content-center align-items-center" @click.self="closeModal">
        <div class="modal-content w-50 rounded d-flex flex-column justify-content-center align-items-center">
            <h3>Edit task</h3>
            <form action="" @submit.prevent="updateTask" class="d-flex column-gap-3">
                <input type="text" :value="taskToEdit.name" ref="editInput">
                <button type="submit" class="btn btn-success">Save</button>
            </form>
        </div>
    </div>
</template>

<script>
    export default {
	name: 'Modal',
    props: ['taskToEdit'],
	methods: {
		updateTask() {
            this.$emit('saved', {
                val: this.$refs.editInput.value ? this.$refs.editInput.value : this.taskToEdit.name
            })
            this.closeModal()
		},

        closeModal() {
            this.$emit('close')
        }
	}

}
</script>

<style>

    .modal-container {
        background-color: #020412e0;
    }

    .modal-content {
        background-color: #363043;
        height: 200px;
    }

</style>