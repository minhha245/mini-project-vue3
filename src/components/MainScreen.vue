<template>
  <div class="screen">
    <h1>POKE</h1>
    <h3>Select</h3>
    <div class="actions">
      <button @click="onStart(9)">
        <span>3*3</span>
        <span>Dễ</span>
      </button>
      <button @click="onStart(16)">
        <span>4*4</span>
        <span>Dễ</span>
      </button>
      <button @click="onStart(36)">
        <span>6*6</span>
        <span>Vừa</span>
      </button>
      <button @click="onStart(48)">
        <span>8*8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10*10</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>
