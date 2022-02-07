<template>
  <div class="category">
    {{ getCategoryPrettyName() }}
  </div>
</template>

<script lang="ts">
import { Component, Prop } from "vue-property-decorator";
import VueWrapper from "../store/VueWrapper";

@Component({
  components: {},
})
export default class Category extends VueWrapper {
  @Prop() public category!: string;

  getCategoryPrettyName(): string {
    if (this.category) {
      const cat = this.$store.state.categories.find(
        (category: any) => category.id === this.category
      );
      if (cat) {
        return cat.title;
      }
    }
    return "";
  }
}
</script>

<style lang="scss">
.category {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  padding: 6px 16px;
  border-radius: 10px;
  background: $eggshellBlue;
  font-weight: 600;
  font-size: 13px;
  color: $royalBlue;
  user-select: none;
}
</style>
