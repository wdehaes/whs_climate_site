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
      <p>flood index 2020: {{flood_20}}</p>
      <p>flood index 2100: {{flood_100}}</p>
      <p>erosion index 2020: {{erosion_20}}</p>
      <p>erosion index 2100: {{erosion_100}}</p>
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
