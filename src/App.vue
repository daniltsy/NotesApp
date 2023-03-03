<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <message v-if="message" :message="message"></message>
          <new-note :note="note" @addNote="addNote"></new-note>
          <div class="note-header" style="margin: 36px 0">
            <h1>{{ title }}</h1>
            <search
              :value="search"
              placeholder="Search your Note"
              @search="search = $event"
            ></search>
            <div class="icons">
              <svg
                style="cursor: pointer"
                :class="{ active: grid }"
                @click="grid = true"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                style="cursor: pointer"
                :class="{ active: !grid }"
                @click="grid = false"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>
          <notes :notes="notesFilter" :grid="grid"></notes>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message"
import notes from "@/components/Notes"
import newNote from "@/components/NewNote"
import search from "@/components/Search"
export default {
  components: {
    message,
    notes,
    newNote,
    search,
  },
  name: "App",
  data() {
    return {
      title: "Notes App",
      message: null,
      grid: true,
      search: "",
      note: {
        title: "",
        descr: "",
      },
      notes: [
        {
          title: "First Note",
          descr: "Description for first note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Second Note",
          descr: "Description for second note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Third Note",
          descr: "Description for third note",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    }
  },
  computed: {
    notesFilter() {
      let notesArray = this.notes,
        search = this.search

      if (!search) return notesArray

      search = search.trim().toLowerCase()
      notesArray = notesArray.filter((el) => {
        if (el.title.toLowerCase().indexOf(search) !== -1) {
          return el
        }
      })
      return notesArray
    },
  },
  methods: {
    addNote() {
      let { title, descr } = this.note

      if (title === "") {
        this.message = "title cant be blank!"
        return false
      }

      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString(),
      })
      this.message = null
      this.note.title = ""
      this.note.descr = ""
    },
  },
}
</script>

<style></style>
