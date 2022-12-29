<template>
    <button @click="execute">{{ buttonText }}</button>
</template>
  
<script>
export default {
    name: 'HitButtons',

    props: {
        buttonText: String,
        callback: {
            type: Function
        }
    },

    data() {
        return {
            
        }
    },

    methods: {
       execute() {
        if (this.callback) {
            this.callback();
        }
       }
    }
}
</script>
  
 
<style lang="scss" scoped>
button {
    @include fontNunito(1.4rem, 800);
    background-color: $color-button;
    color: $color-text-color;
    text-shadow: 1px 1px 10px $color-interface;
    border: none;
    border-radius: 8px;
    padding: 10px 16px;
    min-width: 120px;
    cursor: pointer;
    transition: color, background-color 0.3s;

    &:hover {
        background-color: $color-text-color;
        color: $color-interface;
        text-shadow: none;
        transition: all 0.3s;
    }
}
</style>
  