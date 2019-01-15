<template>
  <div class="banner">
    <h1 class="o-container"><slot></slot></h1>
  </div>
</template>

<script>
export default {
  name: 'Banner'
};
</script>

<style scoped lang="scss">
@import '../styles/settings/spacing';
@import '../styles/settings/color';

.banner { 
  padding: sp(4) 0;
  color: white;
  text-align: center;
  background: linear-gradient(to left,
    color-get(primary) 0%,
    color-get(secondary) 100%
  );
}
</style>
