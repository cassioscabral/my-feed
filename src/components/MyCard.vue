<template>
  <mdl-card class="demo-card-welcome" :title="title" :supporting-text="supportingText" :media="imageUrl" v-if="imageUrl">
  </mdl-card>
</template>
<script>
import Vue from 'vue'
import {
  MdlCard
} from 'vue-mdl'

Vue.use(require('vue-resource'))

function _getYoutubeVideoID (URL) {
  const VIDEO_ID_REGEX = /.*(?:youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=)([^#\&\?]*).*/
  return URL.match(VIDEO_ID_REGEX)[1]
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

export default {
  props: ['title', 'entry', 'type'],
  components: {
    MdlCard
  },
  directives: {
  },
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
      supportingText: 'Support Text'
    }
  },
  methods: {
  },
  computed: {
    imageUrl () {
      if (this.entry.length <= 0) { return }
      // TODO use debounce
      let imageUrl = ''
      if (this.type === 'youtube') {
        // this.title = getYoutubeTitle(this.entry, this.$http)
        return getYoutubePreviewURL(this.entry)
      }
      return imageUrl
    }
  }

}
</script>
<style>
.demo-card-welcome.mdl-card {
  width: 512px;
}
.demo-card-welcome .mdl-card__title,
.demo-card-welcome .mdl-card__menu {
  color: white;
}
.demo-card-welcome .mdl-card__title {
  height: 60px;
  background-color: rgba(85, 0, 249, 0.71);
}
</style>
