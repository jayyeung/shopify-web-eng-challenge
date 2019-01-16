<template>
  <div class="entry">
    <div class="entry__title" @click="onFavourite">
        <div class="entry__star" 
          :class="{'entry__star--fave': this.entry.favourite}">
            <span class="o-icon-star"></span>
        </div>
        <p class="u-mh-3">{{ entry.title }}</p>
    </div>

    <div class="entry__desc" v-html="entry.body">
    </div>
  </div>
</template>

<script>
export default {
  name: "WasteEntry",
  props: { entry: Object },
  methods: {
    onFavourite() {
      const faveVal = !this.entry.favourite;
      this.$emit('favourite', faveVal, this.entry);
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

.entry__star { 
  display: inline-block;
  min-width: 1rem;
  transition: color 0.25s;
  color: color-get(grey);
  &--fave { color: color-get(primary); }
}

.entry__title:hover .entry__star {
  color: darken(color-get(primary), 10);
}
</style>
