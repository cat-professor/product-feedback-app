<template>
  <div class="suggestion-list">
    <suggestion-card
      v-for="suggestion in suggestionList"
      :key="suggestion.id"
      :suggestion="suggestion"
    >
      {{ suggestion }}
    </suggestion-card>
  </div>
</template>

<script lang="ts">
import { Component } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";
import SuggestionCard from "./SuggestionCard.vue";

@Component({
  components: {
    SuggestionCard,
  },
})
export default class SuggestionList extends VueWrapper {
  public suggestionList: any = [];

  mounted() {
    this.suggestionList = this.$store.state.productRequests;
  }
}
</script>

<style lang="scss">
.suggestion-list {
  max-width: 825px;
}
</style>
