<template>
    <div>
        <input type="text" data-accept="[0-9]{5}" :placeholder="placeholderText"  v-model="inputValue" @change="postValue">
    </div>
</template>
  
<script>
export default {
    name: 'TextInput',

    props: {
        placeholderText: String,
    },

    data() {
        return {
            inputValue: undefined,
        }
    },

    methods: {
       postValue() {
           this.$emit('postingValue', this.inputValue);
           this.inputValue = undefined;
       }
    }
}
</script>
  
 
<style lang="scss" scoped>
input {
    @include fontNunito(1.2rem);
    box-sizing: border-box;
    width: 100%;
    border: 1px solid transparent;
    background: $color-bg-100;
    outline: 0;
    color: $color-text-color;
    padding: 10px 16px;
    border-bottom: 1px solid $color-text-color;
    transition: box-shadow 0.3s;

    &::placeholder {
        color: $color-text-color;
        opacity: 0.6;
    }

    &:focus {
        box-shadow: 2px 0px 10px $color-interface;
        transition: all 0.3s;
    }
}
</style>
  