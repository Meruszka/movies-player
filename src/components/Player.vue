<template>
    <video-player
      class="video-player vjs-big-play-centered"
      :src="(`../../public/movies/${path}.mp4`)"
      type="video/mp4"
      crossorigin="anonymous"
      autoplay="play"
      playsinline
      controls
      :volume="0.1"
      :height="320"
      @mounted="handleMounted"
      @timeupdate="handleEvent(player)"
    />
</template>
  
<script lang="ts">
  import { defineComponent, shallowRef } from 'vue'
  import { VideoJsPlayer } from 'video.js'
  import { VideoPlayer } from '@videojs-player/vue'
  import 'video.js/dist/video-js.css'

  export default defineComponent({
    name: 'vue-basic-player-example',
    title: 'Basic player (Vue)',
    components: {
      VideoPlayer
    },
    props:
    {
      path: {
          type: String,
          required: true
      }
    },
    setup() {
      let change = 0;
      const player = shallowRef<VideoJsPlayer>()
      const handleMounted = (payload: any) => {
        player.value = payload.player
      }

      const handleEvent = (player: any) => {
          if (player.hasStarted() && change === 0) {
              change = 1;
              console.log('Początek filmu')
          }
          if (player.currentTime() / player.duration() > 0.5 && change === 1) {
              change = 2;
            console.log('Środek filmu')
          }
          if (player.currentTime() === player.duration() && change === 2) {
              change = 3;
            console.log('Koniec filmu')
          }
      }

      return { player, handleMounted, handleEvent }
    }
  })
</script>
