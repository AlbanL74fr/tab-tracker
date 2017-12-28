<template>
<panel title="YouTube Video">
  <youtube :video-id="youtubeId" :player-width="800" :player-height="330">
  </youtube>
</panel>
</template>

<script>
  // import SongsService from '@/services/SongsService'
  import VueYouTubeEmbed from 'vue-youtube-embed'

  export default {
    props: [
      'youtubeId'
    ],
    components: {
      VueYouTubeEmbed
    }
  }
</script>

<style scoped>
</style>