<template>
  <div class="suggestion-card" tabindex="0">
    <div class="upvotes-container">
      <upvotes
        :upvotes="suggestion.upvotes"
        :suggestionId="suggestion.id"
      ></upvotes>
    </div>
    <div class="suggestion-card-content">
      <h3>{{ suggestion.title }}</h3>
      <p>{{ suggestion.description }}</p>
      <category :category="suggestion.category"></category>
    </div>
    <div class="suggestion-card-comments">
      <svg
        width="18"
        height="16"
        viewBox="0 0 18 16"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M2.62074 16H1.34534L2.24718 15.0895C2.73344 14.5986 3.0371 13.9601 3.11873 13.2674C1.03637 11.8878 0 9.88917 0 7.79388C0 3.92832 3.51913 0 9.0305 0C14.8692 0 18 3.61479 18 7.45522C18 11.321 14.8361 14.9333 9.0305 14.9333C8.0135 14.9333 6.95226 14.7963 6.00478 14.5448C5.10787 15.4735 3.89262 16 2.62074 16Z"
          fill="#CDD2EE"
        />
      </svg>
      {{ getCommentCount() }}
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";
import Category from "./Category.vue";
import Upvotes from "./Upvotes.vue";

@Component({
  components: {
    Upvotes,
    Category,
  },
})
export default class SuggestionCard extends VueWrapper {
  @Prop() public suggestion!: any;

  getCommentCount(): number {
    if (this.suggestion && this.suggestion.comments) {
      return this.suggestion.comments.length;
    }
    return 0;
  }
}
</script>

<style lang="scss">
.suggestion-card {
  display: flex;
  align-items: center;
  background: $suggestionCardBgColor;
  padding: 28px 32px;
  border-radius: 10px;

  &:not(:last-of-type) {
    margin-bottom: 20px;
  }

  &:focus {
    outline: none;
    box-shadow: 0 0 0 2px darken($white, 10%);
  }

  .upvotes-container {
    align-self: baseline;
  }

  .suggestion-card-content {
    width: 100%;
    max-width: 100%;
    margin: 0 40px;
    overflow: hidden;

    p {
      color: $lightGrey;
      font-size: 16px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  }

  .suggestion-card-comments {
    display: flex;
    align-items: center;
    font-size: 16px;
    font-weight: 700;
    letter-spacing: -0.22px;
    flex-shrink: 0;

    svg {
      margin-right: 8px;
    }
  }
}
</style>
