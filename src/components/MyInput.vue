<template>
  <h3>Save something to read/watch/do later</h3>
  <div class="my-input">
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
    :value.sync="myTitle"
    v-show="entry"
  >
  </mdl-textfield>
  <div class="preview-card" v-show="matches">
    <my-card :entry="entry" :title="myTitle" type='youtube'></my-card>
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
      myTitle: ' ' // WITHOUT A VALUE IT DOES NOT RENDERING
    }
  },
  methods: {
    addEntry () {
      window.alert(this.title)
    }
  },
  computed: {
    matches () {
      // TODO matches all kind of links, blog, youtube, etc
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
