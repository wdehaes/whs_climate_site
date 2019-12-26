<template>
<div class="slider-wrapper">
  <vue-slider v-model="value" direction='btt' :height="250" :max="5" :marks="marks2"/>
</div>
</template>

<script>
import VueSlider from 'vue-slider-component'
import 'vue-slider-component/theme/antd.css'
export default {
  components: {
    VueSlider
  },
    data: function () {
      return {
        value: 0,
        marks2: val => val % 1 === 0 ? ({
          label: `${val} → ${10*val}% underwater`,
          labelStyle: {
            opacity: val * 0.9 + 0.5
          },
          labelActiveStyle: {
            color: '#3498db'
          }
        }) : false
      }
    }
};
</script>

<style>
.slider-wrapper {
  margin-top: 20px;
  margin-bottom: 20px;
}
</style>
