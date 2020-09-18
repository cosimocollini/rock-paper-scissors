<template>
    <div class="logo-wrapper">
        <transition name="logo" mode="out-in">
            <img src="../assets/logo.svg" alt="rock-paper-scissors game" v-if="!isVariant" key="classic">
            <img src="../assets/logo-bonus.svg" alt="rock-paper-scissors-lizard-spock game" v-else key="lizard">
        </transition>
    </div>
</template>

<script>
export default {
    name: 'Logo',
    props: {
        isVariant: {
            type: Boolean,
            default: false
        }
    },
}
</script>