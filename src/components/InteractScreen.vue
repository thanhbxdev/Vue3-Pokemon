<template>
  <h1>Interact</h1>
  <card-items
      v-for="(card,index) in cardsContext"
      :key="index"
      :imgBackFaceUrl="`images/${card}.png`"
      :card="{index,value:card}"
      @onFlip="checkRules($event)"
      :ref="`card-${index}`"
  />
</template>

<script>
import CardItems from "@/components/Card";

export default {
  name: "InteractScreen",
  data() {
    return {
      rules: []
    }
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  components: {
    CardItems
  },
  methods: {
    checkRules: function (card) {
      if (this.rules.length === 2) return false

      this.rules.push(card)

      if (this.rules.length === 2 && this.rules[0].value === this.rules[1].value) {
        console.log('right')
      } else if (this.rules.length === 2 && this.rules[0].value !== this.rules[1].value) {
        console.log('wrong')
        setTimeout(() => {
          console.log(123)
          this.$refs[`card-${this.rules[0].index}`].onFlipBack()
          this.$refs[`card-${this.rules[1].index}`].onFlipBack
          this.rules = [];
        }, 800);
      } else {
        return false
      }
    }
  }
}
</script>

<style scoped>

</style>