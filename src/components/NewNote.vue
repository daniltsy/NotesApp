<template>
  <div class="new-note">
    <div class="title-select">
      <div class="title-container">
        <label for="title">Title</label>
        <input v-model="note.title" type="text" id="title" />
      </div>
      <div class="select-container">
        <label for="select">Priority</label>
        <select id="select" v-model="note.priority">
          <option
            v-for="priority in priorities"
            :value="priority"
            :selected="priority === priorities[2]"
          >
            {{ priority }}
          </option>
        </select>
      </div>
    </div>
    <label for="description">Description</label>
    <textarea v-model="note.descr"></textarea>
    <button class="btn btnPrimary" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  name: "NewNote",
  data() {
    return {
      priorities: ["Very Important", "Important", "Normal"],
    }
  },
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note)
    },
  },
}
</script>

<style lang="scss">
.new-note {
  text-align: center;
}
.title-select {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.title-container {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.select-container {
  display: flex;
  flex-direction: column;
  width: 50%;
  margin-left: 20px;
  select {
    padding: 16px 26px;
    margin-bottom: 30px;
    border-radius: 20px;
  }
}
.title-container label,
.select-container label {
  margin-bottom: 5px;
}
</style>
