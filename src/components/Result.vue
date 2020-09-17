<template>
  <div class="result">
      <div
        class="result__coin-wrapper user"
        key="user"
        :class="{ winner: userWin === true }"
      >
        <span>User pick</span>
        <div :class="`coin coin__${selectedCoin}`"></div>
      </div>

      <transition name="fade">
        <div
          class="result__action"
          v-if="userWin == 'draw' || userWin == false || userWin == true"
          key="action"
        >
          <span v-if="userWin != 'draw'">{{
            userWin ? "You Win" : "You Lose"
          }}</span>
          <span v-if="userWin == 'draw'">Draw</span>
          <button class="btn btn__main--white" @click="$emit('resetGame')">Play again</button>
        </div>
      </transition>

      <transition name="fade">
        <div
          class="result__coin-wrapper computer"
          v-if="tableCoin"
          key="computer"
          :class="{ winner: userWin === false }"
        >
          <span>Table pick</span>
          <div :class="`coin coin__${tableCoin}`"></div>
        </div>
      </transition>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: {
    selectedCoin: {
      type: String
    },
    tableCoin: {
      type: String
    },
    userWin: {
      type: [Boolean, String]
    }
  }
};
</script>
