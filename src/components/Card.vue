<template>
  <div class="card">
    <div class="card__inner" :class="{'is-flipped':isFlipped}" @click="onToggle">
      <div class="card__face card__face-front">
        <div class="card__content">
        </div>
      </div>
      <div class="card__face card__face-back">
        <div class="card__content" :style="{backgroundImage:`url(${require('@/assets/'+imgBackFaceUrl)})`}">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardItems",
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true
    },
    card: {
      type: [String, Number, Array, Object]
    }
  },
  data() {
    return {
      isFlipped: false
    }
  },
  methods: {
    onToggle() {
      this.isFlipped = !this.isFlipped
      if (this.isFlipped) this.$emit("onFlip", this.card)
    },
    onFlipBack() {
      this.isFlipped = false
    }
  }
}
</script>

<style scoped>
.card__face-front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 40px 40px;
  height: 100%;
  width: 100%;
}
</style>