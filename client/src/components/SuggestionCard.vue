<template>
  <div class="suggestion-card" tabindex="0">
    <upvotes
      :upvotes="suggestion.upvotes"
      :suggestionId="suggestion.id"
    ></upvotes>
    <div class="suggestion-card-content">
      {{ suggestion.title }}
      {{ suggestion.description }}
      {{ suggestion.category }}
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";
import Upvotes from "./Upvotes.vue";

@Component({
  components: {
    Upvotes,
  },
})
export default class SuggestionCard extends VueWrapper {
  @Prop() public suggestion!: any;
}
</script>

<style lang="scss">
.suggestion-card {
  display: flex;
  background: $suggestionCardBgColor;
  padding: 28px 32px;
  height: 150px;
  border-radius: 10px;

  &:not(:last-of-type) {
    margin-bottom: 20px;
  }

  &:focus {
    outline: none;
    box-shadow: 0 0 0 2px darken($white, 10%);
  }
}
</style>
