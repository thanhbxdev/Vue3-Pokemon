<template>
  <main-screen v-if="statusMatch==='default'" @onStart="onHandleBeforeStart($event)"/>
  <interact-screen v-if="statusMatch==='match'" :cardsContext="settings.cardsContext"/>
  <coppy-screen/>
</template>

<script>
import CoppyrightScreen from '@/components/CoppyrightScreen'
import MainScreen from "@/components/MainScreen";
import InteractScreen from "@/components/InteractScreen";
import {shuffled} from "@/utils/array";

export default {
  name: 'App',
  data() {
    return {
      settings: {
        totalOfBlock: 0,
        cardsContext: [],
        startedAt:null
      },
      statusMatch: "default"
    }
  },
  components: {
    CoppyScreen: CoppyrightScreen,
    MainScreen,
    InteractScreen
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlock = config.totalOfBlock

      const firstCard = Array.from({length: this.settings.totalOfBlock / 2}, (_, i) => i + 1)
      const secondCard = [...firstCard]
      const cards = [...firstCard, ...secondCard]
      this.settings.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))))
      this.settings.startedAt = new Date().getTime()

      this.statusMatch = 'match'
    }
  }
}
</script>
<style lang="scss">
@import './assets/scss/main.scss';
</style>

