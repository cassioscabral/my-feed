<template>
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
  Matches: {{matches}}
  </div>
</template>
<script>
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
    MdlTextfield
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
      buttonClasses: {
        disabled: true,
        colored: true,
        color: 'green'
      }
    }
  },
  methods: {
    addEntry () {
      window.alert(this.entry)
    }
  },
  computed: {
    matches () {
      return YOUTUBE_REGEX.test(this.entry)
    }
  }

}
</script>
<style scoped>
h1 {
  color: #42b983;
}
</style>
