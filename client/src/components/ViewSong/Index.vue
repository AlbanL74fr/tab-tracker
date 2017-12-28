<template>
  <div>
    <v-layout>
      <v-flex xs6>
        <song-metadata :song="song" />
      </v-flex>
      <v-flex xs6 class="ml-2">
        <youtube :youtubeId="song.youtubeId" />
      </v-flex>
    </v-layout>
    <v-layout class="mt-2">
      <v-flex xs6>
        <tab :tab="song.tab" />
      </v-flex>
      <v-flex xs6 class="ml-2">
        <lyrics :lyrics="song.lyrics" />
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
  import SongsService from '@/services/SongsService'
  import SongMetadata from './SongMetadata'
  import Youtube from './Youtube'
  import Lyrics from './Lyrics'
  import Tab from './Tab'

  export default {
    data () {
      return {
        song: null
      }
    },
    async mounted () {
      const songId = this.$store.state.route.params.songId
      this.song = (await SongsService.show(songId)).data
    },
    components: {
      SongMetadata,
      Youtube,
      Lyrics,
      Tab
    }
  }
</script>

<style scoped>
</style>