<template>
  <div class="notes">
    <h1>Notes</h1>
    <div>
      <input v-model="newNote" placeholder="Add a note" @keyup.enter="addNote" />
    </div>
    <div class="actions">
      <button @click="sort = !sort">Toggle sort</button>
    </div>
    <div class="notes">
      <div v-for="note in notes" class="note" :class="{ many: notes.length > 1 }">
        <div class="text">{{ note.text }}</div>
        <div class="actions">
          <button @click="event => removeNote(note)">Delete note</button>
          <span class="date">{{ note.created | date }}</span>
        </div>
      </div>
    </div>
    <div v-observe-visibility="handleVisibility"></div>
    <div v-if="!$subReady.notes" class="loading">Loading...</div>
    <div>{{ firstNote }}</div>
  </div>
</template>

<script>
import { Meteor } from 'meteor/meteor'
import { Notes } from '../api/collections'

export default {
  data () {
    return {
      newNote: '',
      limit: 5,
      sort: true,
    }
  },

  created () {
    // Not SSR friendly (for now)
    this.$subscribe('notes', () => [this.limit])
  },
//
  computed: {
    notes () {
      // Not SSR friendly (for now)
      return this.$autorun(() => Notes.find({}, {
        sort: { created: this.sort ? -1 : 1 },
      }))
    },

    firstNote () {
      return this.notes.length && this.notes[0]
    },
  },

  watch: {
    '$subReady.notes' (value) {
      console.log(value)
    },
  },

  methods: {
    async addNote () {
      if (this.newNote) {
        try {
          await Meteor.callPromise('notes.add', {
            text: this.newNote,
          })
          this.newNote = ''
        } catch (e) {
          console.error(e)
        }
      }
    },

    async removeNote (note) {
      try {
        await Meteor.callPromise('notes.remove', {
          _id: note._id,
        })
      } catch (e) {
        console.error(e)
      }
    },

    handleVisibility (visible) {
      if (visible && this.$subReady.notes) {
        this.limit += 5
      }
    },
  },
}
</script>

<style lang="less" scoped>
.note {
  padding: 32px 0;

  &:not(:last-child) {
    border-bottom: solid 1px fade(black, 10%);
  }

  .text {
    margin-bottom: 12px;
  }

  .date {
    margin-left: 16px;
    color: lighten(black, 70%);
  }
}

input {
  display: block;
  width: 100%;
}

.actions {
  margin-top: 6px;
}
</style>
