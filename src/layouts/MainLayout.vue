<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>
          Listen2gether
        </q-toolbar-title>

        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header>
          Playlist
          <!--  {{ youtubeId }} -->
        </q-item-label>

        <EssentialLink v-for="link in essentialLinks" :key="link.title" v-bind="link" :youtubeId="youtubeId"
          @youtubelink="getYouTubeVideoIdFromUrl" />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref, provide, onBeforeMount } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'A Strange Day',
    caption: 'JiHyo (TWICE)',
    icon: 'school',
    link: 'https://youtu.be/eREbRbw2MJc'
  },
  {
    title: 'Summer Night',
    caption: 'The Boyz',
    icon: 'code',
    link: 'https://youtu.be/X4nzciQm6Rg'
  },
  {
    title: 'A Slow Summer Song',
    caption: 'Fromm',
    icon: 'chat',
    link: 'https://youtu.be/sJ3PnRSLfKw'
  },
  {
    title: 'ZERO MOMENT',
    caption: 'ENHYPEN (Sung by Heesung, Jay, Jake)',
    icon: 'record_voice_over',
    link: 'https://youtu.be/63DLi5ciKn8'
  },
  {
    title: 'I\'ll Wait',
    caption: 'Jiyoon (ICHILLIN\')',
    icon: 'rss_feed',
    link: 'https://youtu.be/drqLGgtPr6c'
  },
  {
    title: 'We Swim in Dreams (Feat. Bang Jaemin)',
    caption: 'tearliner',
    icon: 'public',
    link: 'https://youtu.be/aYUIq3NKDPk'
  },
  {
    title: 'Me, the Protagonist (Feat. Love X Stereo)',
    caption: 'tearliner',
    icon: 'favorite',
    link: 'https://youtu.be/vfWMP1oVUVk'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup() {

    const leftDrawerOpen = ref(false)

    const youtubeId = ref()
    provide('youtubeId', youtubeId)


    onBeforeMount(() => {

      let url = linksList[0].link
      getYouTubeVideoIdFromUrl(url)

    })

    const getYouTubeVideoIdFromUrl = (url) => {

      console.log(url)
      // Our regex pattern to look for a youTube ID
      const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|&v=)([^#&?]*).*/;
      //Match the url with the regex
      const match = url.match(regExp);
      //Return the result
      //return match && match[2].length === 11 ? match[2] : undefined;
      youtubeId.value = match && match[2].length === 11 ? match[2] : undefined;
    };


    return {
      youtubeId,
      getYouTubeVideoIdFromUrl,
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
