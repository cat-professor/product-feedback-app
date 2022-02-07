<template>
  <button
    class="btn"
    :class="getClassList()"
    :disabled="getIsButtonDisabled()"
    @click="onClick"
  >
    <slot></slot>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component({
  components: {},
  props: ["disable", "theme"],
})
export default class SButton extends Vue {
  @Prop() private disable!: boolean;
  @Prop() private theme!: string;

  onClick(e: MouseEvent): void {
    this.$emit("btn-click", e);
  }
  getClassList(): any {
    return {
      "btn-warning": this.theme === "warning",
      "btn-secondary": this.theme === "secondary",
      "btn-cancel": this.theme === "cancel",
    };
  }
  getIsButtonDisabled(): boolean {
    // Undefined disable prop will leave button enabled by default
    return !!this.disable;
  }
}
</script>

<style lang="scss">
.btn {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  padding: 12px 24px;
  border-radius: 10px;
  user-select: none;
  font-size: $btnFontSize;
  position: relative;
  color: $defaultBtnFontColor;
  font-weight: $bold;

  &::before {
    content: "";
    height: 100%;
    width: 100%;
    background: $white;
    border-radius: 10px;
    position: absolute;
    z-index: -1;
    top: 0;
    left: 0;
  }

  @include btnStyles($defaultBtnBgColor);

  &:hover {
    cursor: pointer;
  }

  &:disabled {
    cursor: no-drop;

    &::before {
      background: $disabledBtnFilterBgColor;
    }
  }

  &.btn-warning {
    @include btnStyles($warningBtnBgColor);
  }

  &.btn-secondary {
    @include btnStyles($secondaryBtnBgColor);
  }

  &.btn-cancel {
    @include btnStyles($cancelBtnBgColor);
  }
}
</style>
