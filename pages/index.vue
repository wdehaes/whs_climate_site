<template>
  <div class="pinContainer">
    <div class="container full-page-wrapper">
      <div class="columns is-centered">
        <div class="column is-8 has-text-centered">
          <h1 class="title is-1">
            WHS climate change
          </h1>
          <h2 class="subtitle">
            Willem Dehaes final project FOCJ
          </h2>
        </div>
      </div>
      <div class="columns is-centered">
        <div class="column is-5">
          <p class="text">
            What do a chapel in Ravenna, Italy, a fort in Croatia and a citadel in Algiers have in common? All three monuments are on the UNESCO World Heritage List: they have unique and universal value to humanity. And with the expected rise of the Mediterranean Sea caused by climate change, all three are under increased risk from flooding and erosion.
          </p>
          <p class="text">
            In the face of climate change, researchers have taken an increased interest in its effects on our material heritage. Their motivation is twofold: on the one hand, measuring the vulnerability of these monuments is a necessary step to figure out the best way to adapt them to increases in floods, erosion and extreme temperatures. At the same time, some scientists hope that demonstrating the potential danger to these sites, many of which are ingrained in our collective memory, can help bring forth climate change.
          </p>
          <p class="text">
            Populations can be evacuated, cities rebuilt, but some of these sites, many of which are hundreds or even thousands of years old, might disappear within our lifetime as a result of climate change.
          </p>
        </div>
      </div>
    </div>
    <div class="mapWrapper">
      <Map v-bind:dataset="dataset"></Map>
    </div>
    <div class="explainer-wrapper container full-page-wrapper">
      <div class="columns is-centered">
        <div class="column is-5">
          <div class="has-text-centered">
            <h3 class="title is-4">Measuring risk</h3>
          </div>
        </div>
      </div>
      <div class="columns">
        <div class="column">
          <h4>Flooding</h4>
          <p class="text">Climate change -> Sea level rise -> storm floods worsen</p>
          <p class="text">Risk index: 1 to 10</p>
          <div class="columns">
            <div class="column has-text-centered">
              <p class="text">Area</p>
              <div class="image">
                <img
                  :src="flood"
                  alt="Placeholder image"
                >
              </div>

            </div>

            <div class="column">Flood Height</div>
          </div>
        </div>
        <div class="column">
          <h4>Erosion</h4>
        </div>
      </div>
    </div>
    <div class="container full-page-wrapper">
      <Bell v-bind:whsData='whsAdr'></Bell>
    </div>
    <div class="container cardWrapper">
      <div class="columns is-centered is-multiline">
        <div
          v-for="(monument, index) in whsAdr"
          :key="index"
          class="column is-4"
        >
          <Card v-bind:whs="monument"></Card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from "~/components/Card.vue";
import Bell from "~/components/Bell.vue";
import Map from "~/components/Map.vue";
import * as whs from "~/assets/data/whs.js";

export default {
  data() {
    return {
      dataset: "whs",
      dataset2: "filter",
      whsAdr: whs,
      flood: require("~/assets/img/flood.png")
    };
  },
  mounted() {
    // this.$nextTick(this.pinContainerScene);
  },
  components: {
    Card,
    Bell,
    Map
  },
  methods: {
    pinContainerScene() {
      // Create a new Timeline (equivalent to new TimelineMax())
      const tl = new this.$gsap.TimelineMax({});
      // create scene and set its params
      this.scene = new this.$scrollmagic.Scene({
        triggerElement: ".mapWrapper",
        triggerHook: "onLeave",
        duration: `${2 * 200}%` // each panel animation will last 200% of the screen's height
      })
        .setPin(".pinContainer")
        .setTween(tl);

      // Add scene to ScrollMagic controller by emiting an 'addScene' event on vm.$ksvuescr (which is our global event bus)
      this.$ksvuescr.$emit("addScene", "pinContainerScene", this.scene);
    },
    filterDataset() {
      this.dataset = "filter";
    }
  },
  destroyed() {
    // Destroy ScrollMagic when our component is removed from DOM
    this.$ksvuescr.$emit("destroy");
  }
};
</script>

<style>
.pinContainer {
  width: 100%;
  overflow: hidden;
  position: relative;
}
.full-page-wrapper {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.text {
  margin-bottom: 0.75rem;
}
</style>
