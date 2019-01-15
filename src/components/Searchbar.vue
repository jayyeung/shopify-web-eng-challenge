<template>
  <form class="searchbar" @submit.prevent="onSearch">
    <input class="searchbar__input u-mr-3" 
      type="text" v-model="searchInput"
      placeholder="Type something"/>
      
    <button class="searchbar__button" type="submit">
      <img src="../assets/icon-search.svg"/>
    </button>
  </form>
</template>

<script>
export default {
  name: "Searchbar",
  data: function() {
    return {
      searchInput: ""
    };
  },

  methods: {
    onSearch() {
      this.$emit("search", this.formatedInput);
    }
  },

  computed: {
    formatedInput() {
      return this.searchInput.trim().toLowerCase();
    }
  },

  watch: {
    searchInput(val) {
      // Execute empty search on an empty input
      // (In order to clear list)
      if (val === "") this.onSearch();
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../styles/settings/spacing';

.searchbar {
  display: flex;
  &__input { flex: 1; }
  &__button {
    img { width: $baseline * 17; }
  }
}
</style>
