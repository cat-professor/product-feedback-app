<template>
  <div id="app"><router-view></router-view></div>
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
  public onBtnClick() {}
  mounted() {}
}
</script>

<style lang="scss">
@import "./styles/index.scss";

#app {
  padding: 96px 160px;
}
</style>
