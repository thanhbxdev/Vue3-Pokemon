<template>
  <div
      class="card"
      :class="{disabled:isDisable}"
      :style="{
      height: `${(920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16}px`,
      width: `${
        (((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4
      }px`,
      perspective: `${
        ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4) * 2
      }px`,
    }"
  >
    <div class="card__inner" :class="{'is-flipped':isFlipped}" @click="onToggle">
      <div class="card__face card__face-front">
        <div
            class="card__content"
            :style="{
            'background-size': `${
              (((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) /
              4 /
              3
            }px ${
              (((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) /
              4 /
              3
            }px`,
          }"
        >
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
    },
    cardsContext: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  data() {
    return {
      isDisable: false,
      isFlipped: false
    }
  },
  methods: {
    onToggle() {
      if (this.isDisable) return false
      this.isFlipped = !this.isFlipped
      if (this.isFlipped) this.$emit("onFlip", this.card)
    },
    onFlipBack() {
      this.isFlipped = false
    },
    onEnabledDisabledMode() {
      this.isDisable = true
    }
  }
}
</script>

<style scoped>
.card__face-front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  height: 100%;
  width: 100%;
}
</style>