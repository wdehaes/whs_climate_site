<template>
  <div class="pinContainer">
    <div class="container full-page-wrapper">
      <div class="columns is-centered">
        <div class="column is-8 has-text-centered">
          <h1 class="title is-1">
            History under threat
          </h1>
          <h2 class="subtitle">
            The effects of climate change on the world's cultural heritage
          </h2>
        </div>
      </div>
      <div class="columns is-centered">
        <div class="column is-6">
          <p class="text">
            What do a medieval chapel in Italy, a fort in Croatia and a citadel in Algiers have in common? All three monuments are on the UNESCO World Heritage List: they have a unique and universal value to humanity. And with the expected rise of the Mediterranean Sea caused by climate change, all three are under increased risk from flooding and erosion.
          </p>
          <p class="text">
            In the face of climate change, researchers have taken an increased interest in its effects on our tangible cultural heritage. Their motivation is twofold: on the one hand, measuring the vulnerability of these monuments is a necessary step to figure out the best way to adapt them to increases in floods, erosion and extreme temperatures. At the same time, scientists hope that showing the potential danger to these sites, many of which are ingrained in our collective memory, can help catalyse policy change.
          </p>
          <p class="text">
            Populations can be evacuated, cities rebuilt, but some of these sites, many of which are hundreds or even thousands of years old, might disappear within our lifetime as a result of climate change.
          </p>
        </div>
      </div>
    </div>
    <div class="container full-page-wrapper">
      <div class="columns">
        <div class="column">
          <p class="text">Number of results by publication year when searching for cultural heritage and climate change in the <span class="is-italic">Web of Science</span> online database.</p>
          <Graph v-bind:input="papers"></Graph>
          <p class="text is-size-7">Results from 2019 were excluded, but there were 49 papers as of Dec. 21. There was 1 paper with expected publication date in 2020.</p>
        </div>
        <div class="column">
          <h3 class="title is-4">Expanding Research</h3>
          <p class="text">
            In March 2016, researchers Sandra Fatorić and Erin Seekamp reviewed the literature on cultural heritage and climate change at the time. Using the search functionality in <span class="is-italic">Web of Science</span>, an online scientific database, they found 127 results for the search term <span class="is-italic">"cultural heritag*” AND “climat* chang*"</span>. The same query in December 2019 returned 380 published papers, 217 of which were published since 2016. In other words, more than half of the literature on this topic has been published in the past 4 years.
          </p>
          <p class="text">Part of that rise can be attributed to the increased output of the research community, and both the number of papers on <span class="is-italic">climate change</span> and <span class="is-italic">cultural heritage</span> have been steadily rising, but the increase is nowhere near as pronounced. Chiara Bertolin at the Norwegian university of science and technology confirmed the trend suggested by the data, but pointed out that when looking at the absolute numbers, the impact of climate change on heritage sites is still understudied.</p>
        </div>
      </div>
    </div>
    <div class="container full-page-wrapper">
      <div class="columns">
        <div class="column">
          <h3 class="title is-4">A Broader Scope</h3>
          <p class="text">The list of UNESCO cultural World Heritage Sites encompasses thousands of years of human history across the globe. Factors such as location, age and construction vary wildly between sites, and can make it hard for researchers to generalize findings about vulnerability to climate change.</p>
          <p class="text">Consequently, most research focuses on individual sites or small groups of similar sites. That singular focus allows scientists to dive deep into the site-specific factors ranging from the sensitivity of wooden stave churches in Norway to increased humidity to community needs in flood-phrone Venice. However, that narrow scope comes at a cost. As researchers from the University of Camerino in Italy pointed out in September, as research into the effects of climate change on cultural heritage remains fragmented, so do the efforts to protect it.</p>
          <p class="text">Some scientists decided to take a different approach: studying the effects of global warming on hundreds of sites at the same time. One of them is Lena Reimann, a post-doctoral researcher at the university of Kiel, Germany. In a study published in <span class="is-italic">Nature Communications</span> last year, she analyzed the effects of sea level rise on 159 sites around the Mediterranean coast.</p>
        </div>
        <div class="column"></div>
      </div>
    </div>
    <div class="full-page-wrapper map-wrapper">
      <Map v-bind:dataset="dataset"></Map>
      <div class="card map-overlay">
        <div class="card-content">
          <div class="content">
            <p class="text">
              For every historical site on this map, Reimann calculated the risk of flood and erosion as a result of rising sea levels for every decade between 2000 and 2100. The final result was a risk index between 0 and 10 for each monument. But how did she come up with that number, and what does it mean?
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="explainer-wrapper container full-page-wrapper">
      <div class="columns is-centered">
        <div class="column is-5">
          <div class="has-text-centered">
            <h3 class="title is-4">Determining risk</h3>
          </div>
        </div>
      </div>
      <div class="columns is-centered">
        <div class="column diagram-wrapper">
          <Tree></Tree>
        </div>
        <div class="column">
          <h4 class="title is-6 has-text-centered">Measuring flood damage</h4>
          <p class="text">Reimann measured the effect of a strorm flood that occurs once in a hundred years (a small fraction of their history of many of these monuments). Using storm prediction data and elevation levels across sites, she calculated how much of a site would be underwater if such a storm flood were to happen, and how deep the water would be.</p>

          <!-- <Slider></Slider> -->
          <h4 class="title is-6 has-text-centered">Measuring erosion</h4>
          <p class="text">While floodings are sudden events, erosion chips away at coastal historical sites at a slow, constant pace. The closer a monument is to the coast, the more brittle the soil and the higher the waves, the more it is at risk of erosion. Finally, each tides leaves sediment on the coast, which </p>
          <p class="text">Below are the scales Reimann used to calculate the index for each site.</p>
          <figure class="image">
            <img src="https://media.springernature.com/lw600/springer-static/image/art%3A10.1038%2Fs41467-018-06645-9/MediaObjects/41467_2018_6645_Figa_HTML.png" alt="">
          </figure>
        </div>
      </div>
    </div>
    <div class="container full-page-wrapper">
      <div class="columns is-centered">
        <div class="column is-5">
          <div class="has-text-centered">
            <h3 class="title is-4">The Results</h3>
          </div>
        </div>
      </div>
      <div class="columns is-centered">
        <div class="column is-6">
          <p class="text">The graphs below show the distribution of the flood risk and erosion risk in 2020 and 2100. Each dot represents a site. Click on a dot to see more details about a site.</p>
          <Bell v-bind:whsData='whsAll' density-field-one='column_2020_rcp4_5_flood' density-field-two="column_2100_high_end_flood" svg-id='flood'></Bell>
          <Bell v-bind:whsData='whsAll' density-field-one='column_2020_rcp4_5_erosion' density-field-two="column_2100_high_end_erosion" svg-id='erosion'></Bell>
        </div>
        <div class="column is-6">
          
        </div>
      </div>
      <!-- <Hist v-bind:whsData='whsAll'></Hist> -->
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
import Hist from "~/components/Hist.vue";
import Graph from "~/components/Graph.vue";
import Tree from "~/components/Tree.vue";
import Map from "~/components/Map.vue";
import Slider from "~/components/Slider.vue";
import * as whs from "~/assets/data/whs.js";
import * as whs_full from "~/assets/data/whs_full.js";
import * as erosionData from "~/assets/data/erosion.js"
import * as floodData from "~/assets/data/flood.js";

export default {
  data() {
    return {
      dataset: "whs",
      dataset2: "filter",
      whsAdr: whs,
      whsAll: whs_full,
      flood: floodData,
      erosion: erosionData,
      papers: [
        { year: 2018, value: 60 },
        { year: 2017, value: 53 },
        { year: 2016, value: 54 },
        { year: 2015, value: 51 },
        { year: 2014, value: 19 },
        { year: 2013, value: 20 },
        { year: 2012, value: 12 },
        { year: 2011, value: 16 },
        { year: 2010, value: 8 },
        { year: 2009, value: 6 },
        { year: 2008, value: 12 },
        { year: 2007, value: 5 },
        { year: 2006, value: 8 },
        { year: 2005, value: 1 },
        { year: 2004, value: 2 },
        { year: 2003, value: 2 },
        { year: 1999, value: 1 }
      ]
    };
  },
  mounted() {
    // this.$nextTick(this.pinContainerScene);
  },
  components: {
    Card,
    Bell,
    Hist,
    Graph,
    Tree,
    Map,
    Slider
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
    // this.$ksvuescr.$emit("destroy");
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

.map-wrapper {
  position: relative;
}
.text {
  margin-bottom: 0.75rem;
}

.map-overlay {
  position: absolute;
  left: 5%;
  top: 8%;
  width: 30%;
}

</style>
