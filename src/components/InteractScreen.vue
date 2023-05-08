<template>
  <div class="screen">
    <h1>Tương tác</h1>
    <div class="screen_inner">
      <card-flip
        v-for="(card, index) in cardContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBack="`img/${card}.png`"
        :card="{ index: index, value: card }"
        :rules="rules"
        :cardContext="cardContext"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
</template>

<script>
import CardFlip from "./CardFace.vue";
export default {
  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;

      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("T");
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onEnableFligBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onEnableFligBackCard();
          this.rules = [];
        }, 800);
        const disableEll = document.querySelectorAll(".screen .card.disable");
        if (disableEll && disableEll.length === this.cardContext.length - 2) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 800);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("f");

        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFligBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFligBackCard();

          this.rules = [];
        }, 500);
      } else {
        return false;
      }
    },
  },
};
</script>
<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen_inner {
  width: 440px;
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
