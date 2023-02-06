<template>
  <q-page class="flex flex-center">
    <div>
      <div>

        <button @click="playCurrentVideo">Play</button>
        <button @click="stopCurrentVideo">Stop</button>
        <button @click="pauseCurrentVideo">Pause</button>
      </div>

      <YoutubeVue3 ref="youtube" :videoid="youtubeId" :loop="loop" :autoplay=1 :width="480" :height="320"
        @ended="onEnded" @paused="onPaused" @played="onPlayed" @ready="onReady" />
    </div>
  </q-page>
</template>

<script>
import { ref, inject, defineComponent, onMounted } from 'vue'
import { YoutubeVue3 } from 'youtube-vue3'

export default defineComponent({
  name: 'IndexPage',
  props: {

  },
  emits: ['', ''],
  setup(props, { emit }) {

    const youtube = ref()
    const loop = ref(1)
    const youtubeId = inject('youtubeId')
    // const temp = ref({ video_id: youtubeId, loop: 1 })
    // const play = ref({ video_id: youtubeId, loop: 1 })

    const applyConfig = () => {
      play.value = Object.assign(play, temp)
    }
    const playCurrentVideo = () => {
      youtube.value.player.playVideo();
    }
    const stopCurrentVideo = () => {
      youtube.value.player.stopVideo();
    }
    const pauseCurrentVideo = () => {
      youtube.value.player.pauseVideo();
    }
    const onEnded = () => {
      console.log("## OnEnded")
    }
    const onPaused = () => {
      console.log("## OnPaused")
    }
    const onPlayed = () => {
      console.log("## OnPlayed")
    }

    const onReady = () => {
      // play.value.video_id = youtubeId
      // applyConfig
      // playCurrentVideo
      console.log("## onReady")
    }

    onMounted(() => {
      setTimeout(() => {
        console.log("## onMounted" + youtubeId.value)
        playCurrentVideo()
      }, 1000);


      // https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=3VizND2a9m8&format=json

    })



    return {
      youtube,
      youtubeId,
      loop,
      applyConfig,
      playCurrentVideo,
      stopCurrentVideo,
      pauseCurrentVideo,
      onEnded,
      onPaused,
      onPlayed,
      onReady,
      // temp,
      // play,

    }

  },
  components: {
    YoutubeVue3
  }
})
</script>
