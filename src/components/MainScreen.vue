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

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: #212121;
  color: #f3f3f3;
}
.screen h1 {
  font-size: 4.5rem;
  text-transform: uppercase;
}
.screen p {
  font-size: 2rem;
}
.modes {
  display: flex;
  margin-top: 2rem;
}
.modes button {
  width: 150px;
  height: 150px;
  background: transparent;
  box-shadow: none;
  border: 1px solid #f3f3f3;
  color: #f3f3f3;
  display: flex;
  flex-direction: column;
  border-radius: 1rem;
  margin: 0 1rem;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}
.modes button:hover {
  background-color: #f3f3f3;
  color: #212121;
}
.modes button span:first-child {
  font-size: 2rem;
}
.modes button span:last-child {
  display: block;
  font-size: 1.25rem;
  margin-top: 0.5rem;
}
</style>