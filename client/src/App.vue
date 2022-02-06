<template>
  <div id="app"></div>
</template>

<script lang="ts">
import { Component } from "vue-property-decorator";
import VueWrapper from "./store/VueWrapper";
import SButton from "./components/SButton.vue";

@Component({
  components: {
    SButton,
  },
})
export default class App extends VueWrapper {
  public onBtnClick() {
    console.log("hello");
  }
  mounted() {
    console.log(this.$store.state);
  }
}
</script>

<style lang="scss">
@import "./styles/index.scss";
</style>
