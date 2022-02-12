<template>
  <button class="upvotes" :class="getUpvotesClassList()" @click="onClick">
    <svg
      width="11"
      height="7"
      viewBox="0 0 11 7"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        d="M1.33398 6L5.33398 2L9.33398 6"
        stroke="currentColor"
        stroke-width="2"
      />
    </svg>
    <div class="upvotes-count">{{ upvotes }}</div>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Watch } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";

@Component({
  components: {},
})
export default class Upvotes extends VueWrapper {
  @Prop() public upvotes!: any;
  @Prop() private suggestionId!: string;

  @Watch("$store.state.currentUser.upvoted")
  public watchUpvotedForCurrentUser() {
    this.fetchUpvoteActiveState();
  }

  private upvotesActive: boolean = false;
  public disabled: boolean = true;

  mounted() {
    if (this.$store.getters.getCurrentUser) {
      this.fetchUpvoteActiveState();
    }
  }

  onClick(e: MouseEvent): void {
    this.$store.commit("toggleUpvoteState", this.suggestionId);
  }

  fetchUpvoteActiveState(): void {
    const isUpvoteActive = this.$store.getters.getUpvotesState(
      this.suggestionId
    );
    this.upvotesActive = isUpvoteActive;
  }

  getUpvotesClassList(): any {
    return {
      "upvotes-active": this.upvotesActive,
    };
  }
}
</script>

<style lang="scss">
.upvotes {
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  user-select: none;
  height: 53px;
  max-height: 53px;
  width: 40px;
  max-width: 40px;
  color: $royalBlue;
  background: $eggshellBlue;
  border-radius: 10px;
  flex-shrink: 0;

  & > * {
    pointer-events: none;
  }

  .upvotes-count {
    margin-top: 8px;
    font-size: 13px;
    font-weight: 700;
    letter-spacing: -0.18px;
    color: $mediumGrey;
  }

  &:focus {
    box-shadow: 0 0 0 2px darken($eggshellBlue, 10%);
  }

  &:hover {
    background: $anotherBlue;
    color: $royalBlue;
    cursor: pointer;

    .upvotes-count {
      color: $mediumGrey;
    }
  }

  &.upvotes-active {
    background: $upvotesActiveBgColor;
    color: $white;

    &:hover {
      background: darken($upvotesActiveBgColor, 10%);
    }

    .upvotes-count {
      color: $white;
    }

    &:focus {
      box-shadow: 0 0 0 2px darken($royalBlue, 20%);
    }
  }
}
</style>
