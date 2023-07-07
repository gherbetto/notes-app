<template>
    <div class="new-note">
        <label>Title</label>
        <input v-model="note.title" type="text">
        <label>Priority</label>
        <select v-model="note.priority" name="priority" id="priority-select">
            <option value="">--Please choose an option--</option>
            <option value="low">Low</option>
            <option value="medium">Medium</option>
            <option value="high">High</option>
        </select>
        <label>Description</label>
        <textarea v-model="note.descr"></textarea>
        <button class="btn btnPrimary" @click="addNote" >New Note</button>
    </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true,
        }
    },
    methods: {
        addNote() {
            this.$emit('addNote', this.note)
        }
    }
}

</script>

<style lang="scss">
.new-note {
    text-align: center;
}

select {

}
</style>