<template>
    <div class="wrapper">
        <!--      header-->
        <div class="wrapper-content">
            <section>
                <div class="container">
                    <h1>{{ title }}</h1>

                    <message v-if="message" :message="message"></message>

                    <div class="new-note">
                        <input v-model="note.title" type="text">
                        <textarea v-model="note.descr"></textarea>
                        <button @click="addNote" >New Note</button>
                    </div>
                    <!--    note list   -->
                    <div class="note" v-for="(note, index) in notes" :key="index">
                        <div class="note-header">
                            <p>{{ note.title }}</p>
                        </div>
                        <div class="note-body">
                            <p>{{ note.descr }}</p>
                            <span>{{ note.date }}</span>
                        </div>
                    </div>
                </div>
            </section>
        </div>
        <!--      footer-->
    </div>

</template>

<script>
import message from '@/components/Message.vue'
export default {
    components: {
        message
    },
    data () {
        return {
            title: 'Notes App',
            message: null,
            note: {
                title: '',
                descr: '',
            },
            notes: [
                {
                    title: 'First Note',
                    descr: 'Description for the first note',
                    date: new Date(Date.now()).toLocaleString()
                },
                {
                    title: 'Second Note',
                    descr: 'Description for the second note',
                    date: new Date(Date.now()).toLocaleString()
                },
                {
                    title: 'Third Note',
                    descr: 'Description for the third note',
                    date: new Date(Date.now()).toLocaleString()
                },
            ]
        }
    },
    methods: {
        addNote () {
            let {title, descr} = this.note
            if (title === '') {
                this.message = 'title can`t be blank!'
                return false
            }
            this.notes.push({
                title,
                descr,
                date: new Date(Date.now()).toLocaleString(),
            })
            this.message = null
            this.note.title = ''
            this.note.descr = ''
        }
    }
}
</script>

<style>

</style>
