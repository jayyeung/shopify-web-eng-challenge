<template>
  <div class="entry">
    <div class="entry__title">
      <div @click="onFavourite">
        <div><img class="entry__star" src="../assets/icon-star.svg"/></div>
        <p class="u-mh-3">{{ entry.title }}</p>
      </div>
    </div>

    <div class="entry__desc" v-html="entry.body">
    </div>
  </div>
</template>

<script>
export default {
  name: "WasteEntry",
  props: { entry: Object },
  data: function() {
    return {
      favourite: false
    };
  },
  mounted() {
  },
  methods: {
    onFavourite() { 
      // {...this.entry, favourite: !this.entry.favourite});
      // this.$emit('favourite', entry);
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
