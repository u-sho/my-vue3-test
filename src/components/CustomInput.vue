<template>
  <input class="custom-input" v-model="inputValue" />
  <input
    class="custom-input"
    :value="noAsciiValue"
    @input="$emit('update:noAsciiValue', $event.target.value)"
  />
</template>

<script>
export default {
  inheritAttrs: false,
  props: {
    asciiValue: {
      type: String,
      required: true,
      validator: function(value) {
        return /^[\0-~]*$/.test(value);
      },
    },
    noAsciiValue: {
      type: String,
      default: 'がお',
      required: false,
      validator: function(value) {
        return /^[^\0-~]*$/.test(value);
      },
    },
  },
  emits: ['update:noAsciiValue'],
  computed: {
    inputValue: {
      get() { return this.asciiValue; },
      set(val) { this.$emit("update:asciiValue", val); },
    },
  },
};
</script>

<style scoped>
.custom-input {
  box-sizing: border-box;
  width: 100%;
  height: 2rem;
  font-size: 1.5rem;
  padding: 0 0.5rem;
  line-height: 1;

  border: solid 1px #43ba85;
  border-radius: 4px;
}
.custom-input:focus {
  border: solid 2px #41b883;
  outline: none;
}
</style>