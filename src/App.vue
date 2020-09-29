<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div class="test-area">
    <custom-input
      v-model:ascii-value="state.asciiStr"
      v-model:no-ascii-value="state.noAsciiStr"
      aria-placeholder="ascii, no-ascii"
    />
    <br />
    <button @click="increment">Count is: {{ state.count }}, double is: {{ double[0] }}</button>
    <br />
    <button @click="increment2">Count"1" is: {{ state.count1 }}, double is: {{ double[1]}}</button>
  </div>
  <HelloWorld :msg="state.asciiStr + state.noAsciiStr" />
</template>

<script lang="ts">
import { computed, reactive } from "vue";
import { CustomInput, HelloWorld } from "./components";

export default {
  setup() {
    const state = reactive({
      count: 0,
      count1: 0,
      asciiStr: "",
      noAsciiStr: "",
    });
    const double = computed(() => [
      state.count * 2,
      state.count1 * state.count,
    ]);

    const increment = () => {
      state.count++;
    };
    const increment2 = () => {
      state.count1++;
    };

    return {
      state,
      double,
      increment,
      increment2,
    };
  },
  components: {
    HelloWorld,
    CustomInput,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.test-area {
  width: 300px;
  margin: 1rem auto;
}
.test-area > button {
  box-sizing: border-box;
  width: 100%;
  height: 2rem;
  font-size: 1.5rem;
  margin: 0.5rem 0;

  color: honeydew;
  background-color: #41b883;
  border: none;
  border-radius: 4px;
  padding: 0;
}
</style>
