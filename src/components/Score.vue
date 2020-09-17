<template>
  <div class="score-wrapper">
      <span>Score</span>
      <span>{{ score }}</span>
  </div>
</template>

<script>
export default {
  name: "Score",
  props: {
    score: {
      type: Number,
      default: 0
    }
  }
};
</script>
