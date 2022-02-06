<template>
  <div id="app">
    <s-button :disable="false" @btn-click="onBtnClick">Hello!</s-button>
    <s-button :disable="true" @btn-click="onBtnClick">Hello!</s-button>
    <br />
    <s-button theme="warning" :disable="false" @btn-click="onBtnClick"
      >Hello!</s-button
    >
    <s-button theme="warning" :disable="true" @btn-click="onBtnClick"
      >Hello!</s-button
    >
    <br />
    <s-button theme="secondary" :disable="false" @btn-click="onBtnClick"
      >Hello!</s-button
    >
    <s-button theme="secondary" :disable="true" @btn-click="onBtnClick"
      >Hello!</s-button
    >
    <br />
    <s-button theme="cancel" :disable="false" @btn-click="onBtnClick"
      >Hello!</s-button
    >
    <s-button theme="cancel" :disable="true" @btn-click="onBtnClick"
      >Hello!</s-button
    >
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import SButton from "./components/SButton.vue";

@Component({
  components: {
    SButton,
  },
})
export default class App extends Vue {
  public onBtnClick() {
    console.log("hello");
  }
}
</script>

<style lang="scss">
@import "./styles/index.scss";
</style>
