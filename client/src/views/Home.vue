<template>
  <div id="home">
    <suggestion-list></suggestion-list>
  </div>
</template>

<script>
// @ is an alias to /src
import SuggestionList from "@/components/SuggestionList.vue";

export default {
  name: "Home",
  components: {
    SuggestionList,
  },
};
</script>

<style lang="scss">
#home {
  display: flex;
}
</style>
