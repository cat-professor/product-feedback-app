<template>
  <div class="suggestion-list-container">
    <div class="suggestion-list-actions">
      <logo></logo>
    </div>
    <div class="suggestion-list">
      <suggestions-header
        :count="getSuggestionCount()"
        :selected="sortBy"
      ></suggestions-header>
      <suggestion-card
        v-for="suggestion in suggestionList"
        :key="suggestion.id"
        :suggestion="suggestion"
      >
        {{ suggestion }}
      </suggestion-card>
    </div>
  </div>
</template>

<script lang="ts">
import { Component } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";
import Logo from "./Logo.vue";
import SuggestionCard from "./SuggestionCard.vue";
import SuggestionsHeader from "./SuggestionsHeader.vue";
import { SORT_BY_OPTIONS, SortByOption } from "./SortBy.vue";

@Component({
  components: {
    Logo,
    SuggestionCard,
    SuggestionsHeader,
  },
})
export default class SuggestionList extends VueWrapper {
  public suggestionList: any = [];
  public filterByCategoryId: string = "all";
  public sortBy: SortByOption = SORT_BY_OPTIONS.MOST_UPVOTES;

  mounted() {
    this.suggestionList = this.$store.state.productRequests;
  }

  getSuggestionCount(): number {
    if (this.suggestionList) {
      return this.suggestionList.length;
    }
    return 0;
  }
}
</script>

<style lang="scss">
.suggestion-list-container {
  display: flex;
}
.suggestion-list {
  max-width: 825px;
}
</style>
