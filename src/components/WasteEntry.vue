<template>
  <div class="entry">
    <div class="entry__title">
      <div><img class="entry__star" src="../assets/icon-star.svg"/></div>
      <p class="u-mh-3">{{ title }}</p>
    </div>

    <ul class="entry__desc">
      <slot></slot>
    </ul>
  </div>
</template>

<script>
export default {
  name: "WasteEntry",
  props: { title: String },
  data: function() {
    return {
      favourited: false
    };
  },
  methods: {
    onFavourite() { 
      const favourited = this.data.favourited;
      this.data.favourited = !favourited;
      this.$emit('favourite', !favourited);
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../styles/settings/color';

.entry {
  display: flex;
  &__title { 
    & > * { cursor: pointer; }
    flex: 0.7; 
    display: flex;
    align-items: flex-start;
  }
  &__desc { flex: 0.9; }
}

.entry--favourited {
  .entry__star { color: color-get(primary); }
}
</style>
