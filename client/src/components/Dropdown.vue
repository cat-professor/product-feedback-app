<template>
  <div ref="dropdown" class="dropdown">
    <div class="dropdown-list-item" v-for="listItem in dropdownList">
      {{ listItem.title }}
      <svg
        v-if="getIsSelected(listItem)"
        width="13"
        height="10"
        viewBox="0 0 13 10"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M0.968262 4.85894L4.49995 8.39062L11.9999 0.890625"
          stroke="#AD1FEA"
          stroke-width="2"
        />
      </svg>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";

@Component({
  components: {},
  props: ["dropdownList", "positionElement", "selectedId"],
})
export default class Dropdown extends VueWrapper {
  @Prop() public dropdownList!: any;
  @Prop() private positionElement!: any;
  @Prop() private selectedId!: any;

  mounted(): void {
    // Register dropdown "backdrop" click next tick
    setTimeout(() =>
      document.addEventListener("click", this.onBackdropClick.bind(this))
    );
  }

  unmounted(): void {
    document.removeEventListener("click", this.onBackdropClick.bind(this));
  }

  getIsSelected(selection: any): boolean {
    if (!selection || !selection.id) {
      return false;
    }
    return this.selectedId === selection.id;
  }

  onBackdropClick = (e: MouseEvent) => {
    if (!this.$refs.dropdown) {
      return;
    }
    if (!(<Node>this.$refs.dropdown).contains(<Node>e.target)) {
      this.$emit("close-dropdown");
    }
  };
}
</script>

<style lang="scss">
.dropdown {
  position: fixed;
  min-width: 255px;
  background: $white;
  z-index: 100;
}

.dropdown-list-item {
  display: flex;
  justify-content: space-between;
  padding: 12px 24px;
  color: $lightGrey;

  &:hover {
    cursor: pointer;
    color: $purple;
  }
}
</style>
