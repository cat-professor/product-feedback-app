<template>
  <button class="category-btn">
    {{ category }}
  </button>
</template>

<script lang="ts">
import { Component, Prop, Watch } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";

@Component({
  components: {},
})
export default class Category extends VueWrapper {
  @Prop() public category!: string;
}
</script>

<style lang="scss">
.category-btn {
  padding: 6px 16px;
  border-radius: 10px;
}
</style>
