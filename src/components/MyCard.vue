<template>
  <div id="my-card">
    <div class="mdl-card mdl-shadow--2dp">
      <slot name="title">
        <div class="mdl-card__title" style="background: url('{{titleBackgroundURL}}') center / cover">
          <h2 class="mdl-card__title-text">{{title}}</h2>
        </div>
      </slot>
      <slot name="subtitle" v-if="subtitle">
        <div class="mdl-card__subtitle-text">{{subtitle}}</div>
      </slot>
      <slot name="supporting-text" v-if="note">
        <div class="mdl-card__supporting-text">{{note}}</div>
      </slot>
      <slot name="media" v-if="media">
        <div class="mdl-card__media"><img :src="media"/></div>
      </slot>
      <slot name="actions" v-if="actions">
        <div class="mdl-card__actions mdl-card--border">
          <mdl-anchor-button colored="colored" v-if="isActionsURL" :href="actions" :target="actionsTarget" class="mdl-js-ripple-effect">{{actionsText}}
          </mdl-anchor-button>
          <mdl-button colored="colored" v-else="v-else" class="mdl-js-ripple-effect">{{actionsText}}</mdl-button>
        </div>
      </slot>
      <!-- TODO some way of creating a menu or action-->
      <slot name="menu" v-if="menu">
        <div class="mdl-card__menu">
          <mdl-button icon="icon" @click="triggerMenuEvent" class="mdl-js-ripple-effect"><i class="material-icons">share</i></mdl-button>
        </div>
      </slot>
    </div>
  </div>
</template>
<script>
// import Vue from 'vue'
import {
  MdlCard,
  MdlButton
} from 'vue-mdl'

// Vue.use(require('vue-resource'))

function _getYoutubeVideoID (URL) {
  const VIDEO_ID_REGEX = /.*(?:youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=)([^#\&\?]*).*/
  return VIDEO_ID_REGEX.test(URL) && URL.match(VIDEO_ID_REGEX)[1]
}

// TODO move all the functions getting url to a proper module
function getYoutubePreviewURL (URL) {
  // extract video ID and show get ImageUrl with
  // http://img.youtube.com/vi/<YouTube_Video_ID_HERE>/sddefault.jpg
  let youtubeVideoID = _getYoutubeVideoID(URL)
  if (youtubeVideoID) {
    return `http://img.youtube.com/vi/${youtubeVideoID}/sddefault.jpg`
  }
}

// function getYoutubeTitle (URL, http) {
//   let youtubeVideoID = _getYoutubeVideoID(URL)
//   // GET https://www.googleapis.com/youtube/v3/videos?id=itemId&key=apiKey&fields=items(snippet(title))&part=snippet
//   // alert(data.items[0].snippet.title);
//   http({url: `https://www.googleapis.com/youtube/v3/videos?id=${youtubeVideoID}&key=apiKey&fields=items(snippet(title))&part=snippet`, method: 'GET'}).then(function (response) {
//     return response.items[0].snippet.title
//   }, function (response) {
//     return 'Youtube Title'
//   })
// }
// props: ['title', 'entry', 'type'],
export default {
  props: ['title', 'entry', 'type', 'note'],
  components: {
    MdlCard,
    MdlButton
  },
  directives: {
  },
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
    }
  },
  methods: {
  },
  computed: {
    titleBackgroundURL () {
      // TODO use debounce
      if (this.type === 'youtube') {
        // this.title = getYoutubeTitle(this.entry, this.$http)
        return getYoutubePreviewURL(this.entry)
      }
      return false
    }
  }

}
</script>
<style>
.mdl-card {
  width: 512px;
}
.mdl-card__title,
.mdl-card__menu {
  color: white;
}
.mdl-card__title {
  height: 180px;
  background-color: rgba(85, 0, 249, 0.71);
}
</style>
