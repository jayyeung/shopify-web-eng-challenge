<template>
  <form class="searchbar" @submit.prevent="onSearch">
    <input class="searchbar__input u-mr-3" 
      type="text" v-model="searchInput" 
      :placeholder="placeholder" :disabled="disabled"/>
      
    <button class="searchbar__button" type="submit">
      <span class="o-icon-search"></span>
    </button>
  </form>
</template>

<script>
export default {
  name: "Searchbar",
  props: { 
    disabled: Boolean,
    placeholder: String
  },
  data: function() {
    return {
      searchInput: ""
    };
  },

  methods: {
    onSearch() {
      if (this.disabled) return;
      this.$emit("search", this.formattedInput);
    }
  },

  computed: {
    formattedInput() {
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
  &__button { padding: sp(1); }
}
</style>
