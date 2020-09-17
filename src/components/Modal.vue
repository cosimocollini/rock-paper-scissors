<template>
  <div class="modal">
    <div class="modal__wrapper">
      
      <div class="close" @click="closeModal" v-if="content == 'rules'">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20">
          <path
            fill="#3B4262"
            fill-rule="evenodd"
            d="M16.97 0l2.122 2.121-7.425 7.425 7.425 7.425-2.121 2.12-7.425-7.424-7.425 7.425L0 16.97l7.425-7.425L0 2.121 2.121 0l7.425 7.425L16.971 0z"
            opacity=".25"
          />
        </svg>
      </div>

      <div class="modal__wrapper__header">
        <h1 v-show="content == 'rules'">Rules</h1>
      </div>

      <div class="modal__wrapper__rules" v-if="content == 'rules'">
        <img src="../assets/image-rules.svg" alt="" v-if="!isVariant" />
        <img src="../assets/image-rules-bonus.svg" alt="" v-if="isVariant" />
      </div>

      <div class="modal__wrapper__confirm" v-if="content == 'confirm'">
        <h1>Your score will be reset</h1>
        <div>
          <button class="btn btn__outline--blue" @click="closeModal">
            Cancel
          </button>
          <button class="btn btn__main--blue" @click="confirmChangeGame">
            Confirm
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    content: {
      type: String,
      default: "rules",
      required: false
    },
    isVariant: {
      type: Boolean,
      default: false,
      required: true
    }
  },
  data() {
    return {
      rules: true
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
    confirmChangeGame() {
      this.$emit("confirmChangeGame");
    }
  }
};
</script>
