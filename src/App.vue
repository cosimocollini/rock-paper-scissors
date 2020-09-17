<template>
  <div class="rps">
    <div class="rps__nav">
      <logo :isVariant="isVariant" />
      <score :score="score" />
    </div>

    <div class="rps__coins">
      <transition name="fade" mode="out-in">
        <choose-coin
          :isVariant="isVariant"
          v-if="!selectedCoin"
          @selectCoin="selectCoin"
        />
        <result
          :selectedCoin="selectedCoin"
          v-if="selectedCoin"
          :tableCoin="computerPick"
          :userWin="userWin"
          @resetGame="resetGame"
        />
      </transition>
    </div>

    <div class="rps__actions">
      <button class="btn btn__outline--white change-game" @click="warningScore">
        {{ !isVariant ? "Lizard Spock" : "Classic" }}
      </button>
      <button class="btn btn__outline--white rules" @click="openRules">
        Rules
      </button>
    </div>

    <transition name="fade">
      <modal
        v-if="isModalOpen"
        :isVariant="isVariant"
        :content="modalContent"
        @closeModal="isModalOpen = false"
        @confirmChangeGame="
          isModalOpen = false;
          changeGame();
        "
      />
    </transition>
  </div>
</template>

<script>
import Logo from "./components/Logo";
import Score from "./components/Score";
import Modal from "./components/Modal";
import ChooseCoin from "./components/ChooseCoin";
import Result from "./components/Result";

export default {
  name: "App",
  components: {
    Logo,
    Score,
    Modal,
    ChooseCoin,
    Result
  },
  data() {
    return {
      arr1: ["rock", "paper", "scissors"],
      arr2: ["rock", "paper", "scissors", "lizard", "spock"],
      score: 0,
      userWin: null,
      isVariant: false,
      isModalOpen: false,
      modalContent: "confirm",
      selectedCoin: "",
      computerPick: "",
      animating: false
    };
  },
  methods: {
    openRules() {
      this.modalContent = "rules";
      this.isModalOpen = true;
    },
    openConfirm() {
      this.modalContent = "confirm";
      this.isModalOpen = true;
    },
    warningScore() {
      if (this.animating) return;
      if (this.score > 0 || this.score < 0) {
        this.openConfirm();
      } else {
        this.changeGame();
      }
    },
    changeGame() {
      this.isVariant = !this.isVariant;
      this.score = 0;
    },
    getComputerPick() {
      if (!this.isVariant) {
        let num = Math.floor(Math.random() * 3);
        console.log('TEST', num);
        this.computerPick = this.arr1[num];
      } else {
        this.computerPick = this.arr2[Math.floor(Math.random() * 5)];
      }

      setTimeout(() => {
        this.checkIfUserWin();
      }, 2000);
    },
    selectCoin(e) {
      this.animating = false;
      this.selectedCoin = e;
      setTimeout(() => {
        this.getComputerPick();
      }, 2000);
    },
    updateScore() {
      this.userWin ? (this.score += 1) : (this.score -= 1);
    },
    checkIfUserWin() {
      if (this.selectedCoin == this.computerPick) {
        this.userWin = "draw";
        return;
      }

      if (this.selectedCoin == "rock") {
        this.computerPick == "lizard" || this.computerPick == "scissors"
          ? (this.userWin = true)
          : (this.userWin = false);
      } else if (this.selectedCoin == "paper") {
        this.computerPick == "rock" || this.computerPick == "spock"
          ? (this.userWin = true)
          : (this.userWin = false);
      } else if (this.selectedCoin == "scissors") {
        this.computerPick == "paper" || this.computerPick == "lizard"
          ? (this.userWin = true)
          : (this.userWin = false);
      } else if (this.selectedCoin == "lizard") {
        this.computerPick == "spock" || this.computerPick == "paper"
          ? (this.userWin = true)
          : (this.userWin = false);
      } else if (this.selectedCoin == "spock") {
        this.computerPick == "scissors" || this.computerPick == "rock"
          ? (this.userWin = true)
          : (this.userWin = false);
      }

      this.updateScore();
      this.animating = true;
    },
    resetGame() {
      this.userWin = null;
      this.selectedCoin = "";
      this.computerPick = "";
    }
  },
  mounted() {
    if (window.screen.width < 960) {
      console.log('CIAO', window.innerHeight);
      document.querySelector("body").style.height = `${window.innerHeight}px`;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
