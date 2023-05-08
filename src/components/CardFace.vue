<template>
  <div class="card" :class="{ disable: isDisabled }">
    <div
      class="card_inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard()"
    >
      <div class="card_face card_face-front">
        <div class="card_content"></div>
      </div>
      <div class="card_face card_face-back">
        <div
          class="card_content"
          :style="{
            backgroundImage: `url('${require('@/assets/' + imgBack)}')`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    imgBack: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Object, Array, Number],
    },
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isFlipped: false,
      isDisabled: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onFligBackCard() {
      this.isFlipped = false;
    },
    onEnableFligBackCard() {
      this.isDisabled = true;
    },
  },
};
</script>
<style lang="css" scoped>
.card {
  width: 90px;
  height: 120px;
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}

.card_inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card_inner.is-flipped {
  transform: rotateY(-180deg);
}

.card_face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgb(0, 0, 0, 0.2);
}

.card_face-back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}

.card_face-front .card_content {
  background: url("../assets/img/icon_back.png") no-repeat center center;
  background-size: 40px 40px;
  height: 100%;
  width: 100%;
}

.card_face-back .card_content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}

/* .card.disable .card_inner { */
.card.disable {
  display: none;
  /* cursor: default; */
}
</style>
