<template>
  <div class="screen__inter">
    <div
        class="screen__inner"
        :style="{
          width: `${
            ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-items
          v-for="(card,index) in cardsContext"
          :key="index"
          :imgBackFaceUrl="`images/${card}.png`"
          :card="{index,value:card}"
          :cards-context="cardsContext"
          @onFlip="checkRules($event)"
          :ref="`card-${index}`"
      />
    </div>
  </div>
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
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (
          this.rules.length === 2 &&
          this.rules[0].value === this.rules[1].value
      ) {
        console.log("Right...");
        this.$refs[`card-${this.rules[0].index}`][0].onEnabledDisabledMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnabledDisabledMode();
        this.rules = [];

        const disabledElements = document.querySelectorAll(
            ".screen .card.disabled"
        );
        if (
            disabledElements &&
            disabledElements.length === this.cardsContext.length - 2
        )
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
      } else if (
          this.rules.length === 2 &&
          this.rules[0].value !== this.rules[1].value
      ) {
        console.log("wrong!");
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBack();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBack();
          this.rules = [];
        }, 800);
      } else return false;
    }
  }
}
</script>
