<template>
  <div class="choose-coin">
    <transition name="fade" mode="out-in">
      <div class="choose-coin__classic" v-if="!isVariant" key="classic">
        <img src="../assets/bg-triangle.svg" alt="" />
        <div class="coin coin__rock" name="rock" @click="$emit('selectCoin', $event.target.getAttribute('name'))"></div>
        <div class="coin coin__scissors" name="scissors" @click="$emit('selectCoin', $event.target.getAttribute('name'))"></div>
        <div class="coin coin__paper" name="paper" @click="$emit('selectCoin', $event.target.getAttribute('name'))"></div>
      </div>
      <div class="choose-coin__variant" v-if="isVariant" key="bonus">
        <img src="../assets/bg-pentagon.svg" alt="" />
        <div class="coin coin__rock" name="rock" @click="$emit('selectCoin', $event.target.getAttribute('name'))"></div>
        <div class="coin coin__scissors" name="scissors" @click="$emit('selectCoin', $event.target.getAttribute('name'))"></div>
        <div class="coin coin__paper" name="paper" @click="$emit('selectCoin', $event.target.getAttribute('name'))"></div>
        <div class="coin coin__spock" name="spock" @click="$emit('selectCoin', $event.target.getAttribute('name'))"></div>
        <div class="coin coin__lizard" name="lizard" @click="$emit('selectCoin', $event.target.getAttribute('name'))"></div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "ChooseCoin",
  props: {
    isVariant: {
      type: Boolean,
      default: false,
      required: true
    }
  },
  methods: {
    selectCoin(e) {
      this.$emit("selectCoin", e);
    }
  }
};
</script>
