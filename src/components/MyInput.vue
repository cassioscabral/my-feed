<template>
<div class="my-input">
  <h3>Save something to read/watch/listen/do later</h3>
  Entries: {{entries | json}}
  <br>
  <mdl-textfield
    label="New Entry"
    floating-label="New Entry"
    :value.sync="entry"
    @keyup.enter="addEntry"
  >
  </mdl-textfield>
  <mdl-button
    v-mdl-ripple-effect
    colored
    raised
    primary
    @click="addEntry"
    :disabled="!matches"
  >
  Add
  </mdl-button>
  <br>
  <mdl-textfield
    label="Title"
    floating-label="Title"
    :value.sync="title"
    v-show="entry"
    @keyup.enter="addEntry"
  >
  </mdl-textfield>
  <br>
  <mdl-textfield
    label="Note"
    floating-label="Note"
    :value.sync="note"
    v-show="entry"
    @keyup.enter="addEntry"
  >
  </mdl-textfield>
  <div class="preview-card" v-show="matches">
    <my-card :entry="entry" :title="title" :note="note" type="youtube"></my-card>
  </div>
</div>
</template>
<script>
import MyCard from './MyCard'
import {
  MdlButton,
  MdlTextfield,
  MdlRippleEffect
} from 'vue-mdl'

const YOUTUBE_REGEX = /^(https?\:\/\/)?(www\.)?(youtube\.com|youtu\.?be)\/.+$/i
// TODO
// add props and make the name generic
export default {
  components: {
    MdlButton,
    MdlTextfield,
    MyCard
  },
  directives: {
    MdlRippleEffect
  },
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
      entry: '',
      title: '',
      note: '',
      entries: []
    }
  },
  methods: {
    addEntry () {
      this.entries.push({
        entry: this.entry,
        title: this.title,
        note: this.note
      })
    }
  },
  computed: {
    matches () {
      // TODO should match all kind of links, blog, youtube, podcast, etc
      return YOUTUBE_REGEX.test(this.entry)
    }
  }

}
</script>
<style scoped>
h3 {
  color: #42b983;
}
.preview-card {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
