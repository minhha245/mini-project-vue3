<template>
  <h1>Kết thúc</h1>
  <p>{{ Math.round(timer / 1000) }}giây</p>
  <button @click="onStartAgain">CHơi lại</button>
</template>
<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  emits: ["onStartAgain"],
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>
