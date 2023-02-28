<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1>{{ title }}</h1>
          <message v-if="message" :message="message"></message>
          <new-note :note="note" @addNote="addNote"></new-note>
          <notes :notes="notes"></notes>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message"
import notes from "@/components/Notes"
import newNote from "@/components/NewNote"
export default {
  components: {
    message,
    notes,
    newNote,
  },
  name: "App",
  data() {
    return {
      title: "Notes App",
      message: null,
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
