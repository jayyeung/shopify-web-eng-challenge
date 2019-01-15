<template>
  <div id="app">
    <banner>Toronto Waste Lookup</banner>

    <!-- Main Section -->
    <div id="main" class="u-mb-5">
      <searchbar class="u-mt-3 u-mb-4"
        @search="handleSearch"/>

      <div class="waste-entries">
        <waste-entry v-for="(res, i) in searchRes" 
          :title="res.title" :key='`result-${i}`'>

          <li>Empty and rinse (if necessary and possible) this item before placing it in the Blue Bin.</li>
          <li>Any type of black or compostable plastic is not accepted and should be placed in the Garbage Bin.</li>
        </waste-entry>
      </div>
    </div> 

    <!-- Favourite Section -->
    <div id="faves">
      <div class="o-container">
        <h2>Favourites</h2>

        <div class="waste-entries u-mt-4">
          <waste-entry title="Blue Bin (plastic takeout food and produce containers)">
            <li>Empty and rinse (if necessary and possible) this item before placing it in the Blue Bin.</li>
            <li>Any type of black or compostable plastic is not accepted and should be placed in the Garbage Bin.</li>
          </waste-entry>
        </div>
      </div>
    </div>
  </div>
</template>

<script>  
import Banner from './components/Banner.vue';
import WasteEntry from './components/WasteEntry.vue';
import Searchbar from './components/Searchbar.vue';

const API = 'https://secure.toronto.ca/cc_sr_v1/data/swm_waste_wizard_APR?limit=1000';

export default {
  name: 'app',
  components: { Banner, WasteEntry, Searchbar },
  data: function() {
    return {
      loaded: false,
      query: "",
      apiData: [],
      searchRes: [],
      favourites: []
    };
  },

  // prefetch data to be searched
  mounted() {
    this.$http.get(API)
      .then((res) => { this.apiData = res.data; this.loaded = true; })
      .catch((err) => {
        console.error("Fetching error occured:", err);
        alert("There was an error fetching the data. Please refresh the page and try again.");
    });
  },

  methods: {
    handleSearch(val) {
      if (val === this.query) return;
      if (val === "") this.searchRes = [];
      else this.searchRes = this.apiData.filter((ent) => (
        ent.keywords.toLowerCase().includes(val) ||
        ent.title.toLowerCase().includes(val)
      ));
      this.query = val;
    }
  }

}
</script>

<style lang="scss">
@import './styles/main.scss';

#app {
  height: 100vh;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
}

#main { @extend .o-container; }

#faves {
  flex: 1;
  padding: sp(4) 0 sp(5);
  background: lighten(color-get(primary), 61);
  color: color-get(primary);
}

.waste-entries {
  color: initial;
  & > *:not(:last-child) {
    margin-bottom: sp(5);
  }
}
</style>
