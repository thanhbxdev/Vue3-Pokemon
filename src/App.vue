<template>
  <main-screen v-if="statusMatch==='default'" @onStart="onHandleBeforeStart($event)"/>
  <interact-screen
      v-if="statusMatch==='match'"
      :cardsContext="settings.cardsContext"
      @onFinish="onGetResult"
  />
  <result-screen
      v-if="statusMatch==='result'"
      :timer="timer"
      @onStartAgain="statusMatch='default'"
  />
  <coppy-screen/>
</template>

<script>
import CoppyrightScreen from '@/components/CoppyrightScreen'
import MainScreen from "@/components/MainScreen";
import InteractScreen from "@/components/InteractScreen";
import {shuffled} from "@/utils/array";
import ResultScreen from "@/components/ResultScreen";

export default {
  name: 'App',
  components: {
    CoppyScreen: CoppyrightScreen,
    MainScreen,
    InteractScreen,
    ResultScreen
  },
  data() {
    return {
      settings: {
        totalOfBlock: 0,
        cardsContext: [],
        startedAt:null
      },
      statusMatch: "default",
      timer:0
    }
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
    },
    onGetResult(){
      console.log(123)
      this.timer= new Date().getTime() -this.settings.startedAt
      this.statusMatch = 'result'
    }
  }
}
</script>
<style lang="scss">
@import './assets/scss/main.scss';
</style>

