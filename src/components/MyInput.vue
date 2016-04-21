<template>
  <div class="my-input">
    <mdl-textfield label="New Entry" floating-label="New Entry" :value.sync="entry"></mdl-textfield>
    <mdl-button v-mdl-ripple-effect @click="addEntry">Add</mdl-button>
  </div>
</template>
<script>
import {
  MdlButton,
  MdlTextfield
} from 'vue-mdl'
// TODO
// add props and make the name generic
export default {
  components: {
    MdlButton,
    MdlTextfield
  },
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
      entry: ''
    }
  },
  methods: {
    addEntry () {
      window.alert(this.entry)
    }
  }

}
</script>
<style scoped>
h1 {
  color: #42b983;
}
</style>
