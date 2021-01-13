<template>
  <slot name="head">
    <h4>Testing Area</h4>
  </slot>
  <input
    ref="asciiInput"
    v-model="inputValue"
    class="custom-input"
  >
  <slot :displayValue="'ascii: ' + asciiValue.toLowerCase()">
    <div class="vspace" />
  </slot>
  <input
    class="custom-input"
    :value="noAsciiValue"
    @input="$emit('update:noAsciiValue', $event.target.value)"
  >
  <slot
    name="foot"
    :displayValue="'no-ascii: ' + noAsciiValue"
  />
</template>

<script lang="ts">
export default {
  inheritAttrs: false,
  props: {
    asciiValue: {
      type: String,
      required: true,
      validator: (value: Readonly<string>) => /^[\0-~]*$/.test(value),
    },
    asciiValueModifiers: null,
    noAsciiValue: {
      type: String,
      default: 'がお',
      required: false,
      validator: function(value: Readonly<string>) {
        return /^[^\0-~]*$/.test(value);
      },
    },
  },
  emits: {
    'update:asciiValue': (asciiValue: Readonly<string>) => /^[\0-~]*$/.test(asciiValue),
    'update:noAsciiValue': (noAsciiValue: Readonly<string>) => /^[^\0-~]*$/.test(noAsciiValue),
  },
  computed: {
    inputValue: {
      get(): string {
        return this.asciiValue;
      },
      set(val: string) {
        let value = val;
        if (this.asciiValueModifiers.capitalize) {
          value = value.toUpperCase();
        }
        this.$emit("update:asciiValue", value);
      },
    },
  },
  mounted() {
    (this.$refs.asciiInput as HTMLInputElement).focus();
  },
};
</script>

<style scoped>
.custom-input {
  box-sizing: border-box;
  width: 100%;
  height: 2rem;
  border: solid 1px #43ba85;
  border-radius: 4px;
  padding: 0 0.5rem;

  font-size: 1.5rem;
  line-height: 1;
}
.custom-input:focus {
  border: solid 2px #41b883;
  outline: none;
}
.vspace {
  box-sizing: border-box;
  height: 0;
  width: 0;
  margin: 0.1rem 0;
  border: none;
  padding: 0;
}
</style>