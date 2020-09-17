<template>
    <div class="logo-wrapper">
        <transition name="logo" mode="out-in">
            <img src="../assets/logo.svg" v-if="!isVariant" key="classic">
            <img src="../assets/logo-bonus.svg" v-else key="lizard">
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