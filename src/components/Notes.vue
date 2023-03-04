<template>
  <div class="notes">
    <div
      class="note"
      :class="{ full: !grid }"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div
        class="note-header"
        :class="[{ full: !grid }, getClass(note)]"
        @dblclick="showHiddenInput(index)"
      >
        <p v-if="activeIndex !== index">{{ note.title }}</p>
        <input
          v-if="activeIndex === index"
          type="text"
          v-model="note.title"
          @keydown="updateNoteTitle(index, $event)"
          @blur="canselEditing(index)"
        />
        <p style="cursor: pointer" @click="removeNote(index)">x</p>
      </div>
      <div class="note-body">
        <p>{{ note.descr }}</p>
        <span> {{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Notes",
  data() {
    return {
      hiddenInput: false,
      activeIndex: null,
      initialTitle: "",
      noBlur: false,
    }
  },
  props: {
    notes: {
      type: Array,
      required: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    removeNote(index) {
      this.notes.splice(index, 1)
    },
    getClass(note) {
      if (note.priority === "Very Important") return "red"
      else if (note.priority === "Important") return "orange"
      else return "green"
    },
    showHiddenInput(index) {
      this.activeIndex = index
      this.hiddenInput = !this.hiddenInput
      this.initialTitle = this.notes[index].title
      this.noBlur = false
    },
    updateNoteTitle(index, event) {
      if (event.keyCode === 13) {
        this.notes[index].title = this.notes[index].title.trim()
        this.activeIndex = null
        this.hiddenInput = false
        this.noBlur = true
      } else if (event.keyCode === 27) {
        this.canselEditing(index)
      }
    },
    canselEditing(index) {
      if (!this.noBlur) {
        this.notes[index].title = this.initialTitle
        this.activeIndex = null
        this.hiddenInput = false
      }
    },
  },
}
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 48%;
  padding: 10px 20px;
  margin-bottom: 20px;
  background-color: white;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.02);
  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
    transform: translate(0, -10px);
    transition-delay: 0s !important;
  }
  &.full {
    width: 100%;
    text-align: center;
  }
}
.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  h1 {
    font-size: 32px;
  }
  p {
    color: mediumblue;
  }
  input {
    margin-bottom: 0px;
    padding: 0px;
  }
  svg {
    margin-right: 12px;
    color: #999999;
    &.active {
      color: blue;
    }
    &:last-child {
      margin-right: 0;
    }
  }
  &.full {
    justify-content: center;
    p {
      margin-right: 16px;
      &:last-child {
        margin-right: 0;
      }
    }
  }
  &.red {
    p {
      color: red;
    }
  }
  &.orange {
    p {
      color: orange;
    }
  }
  &.green {
    p {
      color: green;
    }
  }
}
.note-body {
  p {
    margin: 20px 0;
    font-size: 14px;
    color: #999999;
  }
  span {
    font-size: 14px;
  }
}
</style>
