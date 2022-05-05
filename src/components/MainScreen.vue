<template>
  <div class="screen">
    <h1 class="main__title">pokemon memories</h1>
    <p class="main__content">select mode to start game</p>
    <div class="actions">
      <button v-for="item in items" @click="onStart(item.quantity**2)" v-bind:key="item">
        <p class="actions__quantity">{{ item.quantity }} x {{ item.quantity }}</p>
        <p class="actions__level">{{ item.level }}</p>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainScreen",
  data() {
    return {
      items: [
        {quantity: 4, level: 'easy'},
        {quantity: 6, level: 'normal'},
        {quantity: 8, level: 'hard'},
        {quantity: 10, level: 'super hard'},
      ]
    }
  },
  methods: {
    onStart(totalOfBlock) {
      this.$emit("onStart", {totalOfBlock})
    }
  }
}
</script>

<style scoped>

</style>