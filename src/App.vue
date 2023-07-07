<template>
    <div class="wrapper">
        <div class="wrapper-content">
            <section>
                <div class="container">
                    <!--message-->
                    <message v-if="message" :message="message"></message>
                    <!--new note-->
                    <newNote :note="note" @addNote="addNote"></newNote>
                    <!--title-->
                    <div class="note-header" style="margin: 36px 0">
                        <h1>{{ title }}</h1>
                        <search :value="search" placeholder="Find your note" @search="search = $event"></search>
                    <!--icons controls-->
                        <div class="icons">
                            <svg :class="{ active: grid }" @click="grid = true" style="cursor: pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
                            <svg :class="{ active: !grid }" @click="grid = false" style="cursor: pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
                        </div>
                    </div>
                    <!--note list-->
                    <notes :priority="notes.priority" :notes="notesFilter" :grid="grid" @remove="removeNote"></notes>

                </div>
            </section>
        </div>
    </div>

</template>

<script>
import message from '@/components/Message.vue'
import notes from '@/components/Notes.vue'
import newNote from '@/components/NewNote.vue'
import search from '@/components/Search.vue'

export default {
    components: {
        message, notes, newNote, search
    },
    data () {
        return {
            title: 'Notes App',
            search: '',
            message: null,
            grid: true,
            note: {
                title: '',
                priority: '',
                descr: '',
            },
            notes: [
                {
                    title: 'First Note',
                    priority: 'low',
                    descr: 'Description for the first note',
                    date: new Date(Date.now()).toLocaleString()
                },
                {
                    title: 'Second Note',
                    priority: 'medium',
                    descr: 'Description for the second note',
                    date: new Date(Date.now()).toLocaleString()
                },
                {
                    title: 'Third Note',
                    priority: 'high',
                    descr: 'Description for the third note',
                    date: new Date(Date.now()).toLocaleString()
                },
            ]
        }
    },
    computed: {
        notesFilter () {
            let array = this.notes,
                search = this.search
            if (!search) return array
            // lower
            search = search.trim().toLowerCase()
            // filter
            array = array.filter(function (item) {
                if (item.title.toLowerCase().indexOf(search) !== -1) {
                return item
                }
            })
            // error
            return array
        }
    },
    methods: {
        addNote () {
            let {title, priority, descr} = this.note
            if (title === '' || priority === '' ) {
                this.message = 'title or priority can`t be blank!'
                return false
            }
            this.notes.push({
                title,
                priority,
                descr,
                date: new Date(Date.now()).toLocaleString(),
            })
            this.message = null
            this.note.title = ''
            this.note.priority = ''
            this.note.descr = ''
        },
        removeNote (index) {
            this.notes.splice(index, 1)
        }
    }
}
</script>

<style>

</style>
