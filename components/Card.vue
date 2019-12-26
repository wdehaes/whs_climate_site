<template>
  <div class="card">
  <div class="card-image">
    <figure class="image is-4by3">
      <img :src="url" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="content">
      <h4>{{name}}</h4>
      <div class="columns">
        <div class="column">
          <p class="heading">2020</p>
          <p class="text">Flood index: {{flood_20}}</p>
          <p class="text has-text-right">height: 2ft</p>
          <p class="text has-text-right"> 40 %under water</p>
          <p class="text">Erosion index: {{erosion_20}}</p>
          <p class="text has-text-right">2000ft from coast</p>
          <p class="text has-text-right">material</p>
        </div>
        <div class="column">
          <p class="heading">2100</p>
          <p class="text">Flood index: {{flood_100}}</p>
          <p class="text has-text-right">height: 2ft</p>
          <p class="text has-text-right"> 40 %under water</p>
          <p class="text">Erosion index: {{erosion_100}}</p>
          <p class="text has-text-right">2000ft from coast</p>
          <p class="text has-text-right">material</p>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: {
    whs: Object
  },
  computed: {
    name() {
      return this.whs.name_en;
    },
    flood_20() {
      return this.whs.column_2020_rcp8_5_flood;
    },
    flood_100() {
      return this.whs.column_2100_rcp8_5_flood;
    },
    erosion_20() {
      return this.whs.column_2020_rcp8_5_erosion;
    },
    erosion_100() {
      return this.whs.column_2100_rcp8_5_erosion;
    },
    url() {
      const siteId = String(this.whs.id_no);
      const url = require('~/assets/img/site_' + siteId.padStart(4, '0') + '.jpg');
      return url
    }
  },
}
</script>

<style>

</style>
