<template>
  <div class="sort-by" :class="{ open: dropdownOpen }" @click="onSortByClick()">
    <span>Sort by:</span>
    <div ref="selectedSortBy" class="selected-sort-by">
      {{ prettyNameSelectedSortBy(selected) }}
      <svg
        v-if="dropdownOpen"
        class="arrow-up"
        width="9"
        height="7"
        viewBox="0 0 9 7"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path d="M1 6L5 2L9 6" stroke="white" stroke-width="2" />
      </svg>
      <svg
        v-if="!dropdownOpen"
        class="arrow-down"
        width="9"
        height="7"
        viewBox="0 0 9 7"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path d="M1 1L5 5L9 1" stroke="white" stroke-width="2" />
      </svg>
      <dropdown
        v-if="dropdownOpen"
        :dropdownList="sortByOptions"
        :selectedId="selected.id"
        :positionElement="$refs.selectedSortBy"
        @close-dropdown="onClose"
      ></dropdown>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";
import Dropdown from "./Dropdown.vue";

interface SortByOptions {
  [key: string]: SortByOption;
}

export interface SortByOption {
  id: string;
  title: string;
}

export const SORT_BY_OPTIONS: SortByOptions = {
  MOST_UPVOTES: {
    id: "mostUpvotes",
    title: "Most Upvotes",
  },
  LEAST_UPVOTES: {
    id: "leastUpvotes",
    title: "Least Upvotes",
  },
  MOST_COMMENTS: {
    id: "mostComments",
    title: "Most Comments",
  },
  LEAST_COMMENTS: {
    id: "leastComments",
    title: "Least Comments",
  },
};

@Component({
  components: {
    Dropdown,
  },
  props: ["selected"],
})
export default class SortBy extends VueWrapper {
  @Prop() public selected!: SortByOption;

  public dropdownOpen: boolean = false;
  public sortByOptions = SORT_BY_OPTIONS;

  public prettyNameSelectedSortBy(selection: SortByOption): string {
    if (selection.title) {
      return selection.title;
    }
    return "";
  }

  public onSortByClick(): void {
    this.toggleDropdown();
  }

  private toggleDropdown(): void {
    this.dropdownOpen = !this.dropdownOpen;
  }

  public onClose(): void {
    this.dropdownOpen = false;
  }
}
</script>

<style lang="scss">
.sort-by {
  user-select: none;
}
</style>
