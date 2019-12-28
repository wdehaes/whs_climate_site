<template>
  <div class="pinContainer" ref="pin">
    <section class="panel panel-0"><div class="containe">
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
    </section>
    <section class="panel panel-1"><div class="container">
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
    </section>
    <section class="panel panel-2"><div class="container">
      <div class="columns">
        <div class="column">
          <h3 class="title is-4">A Broader Scope</h3>
          <p class="text">The list of UNESCO cultural World Heritage Sites encompasses thousands of years of human history across the globe. Factors such as location, age and construction vary wildly between sites, and can make it hard for researchers to generalize findings about vulnerability to climate change.</p>
          <p class="text">Consequently, most research focuses on individual sites or small groups of similar sites. That singular focus allows scientists to dive deep into the site-specific factors ranging from the sensitivity to increased humidity of wooden stave churches in Norway to community needs in flood-prone Venice. However, that narrow scope comes at a cost. As researchers from the University of Camerino in Italy pointed out in September, as research into the effects of climate change on cultural heritage remains fragmented, so do the efforts to protect it.</p>
          <p class="text">Some scientists decided to take a different approach: studying the effects of global warming on hundreds of sites at the same time. One of them is Lena Reimann, a post-doctoral researcher at the university of Kiel, Germany. In a study published in <span class="is-italic">Nature Communications</span> last year, she analyzed the effects of sea level rise on 159 sites around the Mediterranean coast.</p>
        </div>
        <div class="column">
          <p class="text is-size-7">Sensors placed on two stave churches in Norway measure the outside conditions. Additional sensors show the conditions inside. <span class="is-italic"> Credit: <a href="https://www.ntnu.edu/symbol/start" target="_blank" rel="noopener noreferrer">NTNU Symbol project</a>
            </span> </p>
          <img src="https://www.ntnu.edu/documents/1279139661/0/Bilde1.jpg/c67f4700-cbe7-61f0-d5bb-a3994206e596?t=1573130023313&imagePreview=1" alt="">
          <p class="text is-size-7">View of New Lamark, an industrial heritage site in Scotland part of a study proposing a more community-inclusive approach for assessing its vulnerability.<span class="is-italic"> Credit:<a href='https://pxhere.com/fr/photo/269222' target="_blank" rel="noopener noreferrer"> pxhere </a></span></p>
          <img :src="lamark" alt="">
        </div>
      </div>
      </div>
    </section>
    <section class="map-wrapper panel panel-3">
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
    </section>
    <section class="panel panel-4"><div class="container">
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
          <p class="text">While floodings are sudden events, erosion chips away at coastal historical sites at a slow, constant pace. The closer a monument is to the coast, the more brittle the soil and the higher the waves, the more it is at risk of erosion. Finally, each tide leaves sediment on the coast, which counteracts erosion (i.e. more sediment disposed lowers the risk of erosion).</p>
          <p class="text">Below are the scales Reimann used to calculate the index for each site.</p>
          <div class="columns">
            <div class="column is-10">

              <figure class="image">
                <img
                  src="https://media.springernature.com/lw600/springer-static/image/art%3A10.1038%2Fs41467-018-06645-9/MediaObjects/41467_2018_6645_Figa_HTML.png"
                  alt=""
                >
              </figure>
            </div>
          </div>
        </div>
      </div>
      </div>
    </section>
    <section class="panel panel-5"><div class="container">
      <div class="columns is-centered">
        <div class="column is-5">
          <h3 class="title is-4 has-text-centered">The Results</h3>
        </div>
      </div>
      <div class="columns is-centered">
        <div class="column is-6">
          <p class="text">Distribution of the flood risk index over all 151 historic sites.</p>
          <Bell
            v-bind:whsData='whsAll'
            density-field-one='column_2020_rcp4_5_flood'
            v-bind:density-field-two="activeScenarioFlood"
            svg-id='flood'
          ></Bell>
          <p class="text">Distribution of the erosion risk index over all 151 historic sites.</p>
          <Bell
            v-bind:whsData='whsAll'
            density-field-one='column_2020_rcp4_5_erosion'
            v-bind:density-field-two="activeScenarioErosion"
            svg-id='erosion'
          ></Bell>
        </div>
        <div class="column is-6">
          <bulma-accordion initial-open-item="1">
            <bulma-accordion-item>
              <h4 slot="title">Description</h4>
              <div slot="content">
              <p class="text">These graphs show the distribution of the flood risk and erosion risk in 2020 and the prediction in 2100. The future risks are based on predictions made by the United Nations' Intergovernmental Panel on Climate Change (IPCC). These predictions are devided into four pathways based on the amount of greenhouse gases humans will emit in the years and decades to come. Scenarios with higher emissions and more extreme temperature rises will lead to higher sea levels, and as a result, to higher risks of flood and erosion. In addition, each scenario represents a range of potential sea level rises. While she calculated the risks under all four scenarios, Reimann uses for the maps and graphs in her work is the high-end estimate under the most extreme of the four pathways, called RCP8.5.</p>
              <p class="text">Reimann pointed out thet the IPCC scenarios might underestimate the sea level rise because they do not sufficiently take account melting land ice. More importantly, she decided to illustrate the more extreme scenario because data is only available until 2100, and she wanted to illustrate what could happen in the 22nd century as well. In other words, if in her calculations a site reaches a risk factor 10 in 2100, it might reach it a few decades later, but it will reach that extreme risk, and a few decades are insignificant in the history of many of these heritage sites.</p>
              <p class="text">
                To give an idea of the predicted risks under the different scenarios, you can switch scenarios and the graphs will show the risk distribution in 2100 under each scenario.
              </p>
              </div>

            </bulma-accordion-item>
            <bulma-accordion-item>
              <h4 slot="title">Scenarios</h4>
              <div class="scenario-selection" slot="content">
                <p class="text">Below are the names of the different scenarios, predicted temperature rise in &#8451; and sea level rise in meters. The horizontal bar represents the range of estimates, and the vertical line the estimate Reimann used in her research.</p>
                <div class="columns">
                  <div class="column">Scenario</div>
                  <div class="column"><figure class="image is-48x48">
                    <img v-bind:src="tempIcon" alt="" class="scenarioIcon"></figure></div>
                  <div class="column"><figure class="image is-48x48">
                    <img v-bind:src="seaIcon" alt="" class="scenarioIcon"></figure></div>
                </div>
                <div
                  v-for="scenario in scenarios"
                  :key="scenario.field"
                  class="columns"
                >
                  <div class="column is-4">

                  <label class="radio">
                    <input
                      type="radio"
                      v-bind:id="scenario.field"
                      v-bind:value="scenario.field"
                      v-model="activeScenario"
                    >
                    {{scenario.name}}
                    </label>
                  </div>
                  <div class="column is-8">
                    <ScenarioDetails v-bind="scenario"></ScenarioDetails>
                  </div>

                </div>
              </div>
            </bulma-accordion-item>
          </bulma-accordion>
        </div>
      </div>
      </div>
    </section>

    <!-- <div class="container full-page-wrapper">
      <div class="columns is-centered">
        <div class="column is-5">
          <h3 class="title is-4 has-text-centered">The Results</h3>
        </div>
      </div>
    </div> -->
    <!-- <div class="container cardWrapper">
      <div class="columns is-centered is-multiline">
        <div
          v-for="(monument, index) in whsAdr"
          :key="index"
          class="column is-4"
        >
          <Card v-bind:whs="monument"></Card>
        </div>
      </div>
    </div> -->
  </div>
</template>

<script>
import Card from "~/components/Card.vue";
import Bell from "~/components/Bell.vue";
import Hist from "~/components/Hist.vue";
import Graph from "~/components/Graph.vue";
import Tree from "~/components/Tree.vue";
import ScenarioDetails from "~/components/ScenarioDetails.vue";
import Map from "~/components/Map.vue";
import Slider from "~/components/Slider.vue";
import * as whs from "~/assets/data/whs.js";
import * as whs_full from "~/assets/data/whs_full.js";
import * as erosionData from "~/assets/data/erosion.js";
import * as floodData from "~/assets/data/flood.js";
import { BulmaAccordion, BulmaAccordionItem } from "vue-bulma-accordion";
export default {
  data() {
    return {
      dataset: "whs",
      dataset2: "filter",
      whsAdr: whs,
      whsAll: whs_full,
      flood: floodData,
      erosion: erosionData,
      activeScenario: "column_2100_high_end",
      scene: {},
      scenarios: [
        {
          name: "RCP2.6",
          tMean: 1.0,
          tLow: 0.3,
          tHigh: 1.7,
          sMean: 0.4,
          sLow: 0.26,
          sHigh: 0.55,
          field: "column_2100_rcp2_6"
        },
        {
          name: "RCP4.5",
          tMean: 1.8,
          tLow: 1.1,
          tHigh: 2.6,
          sMean: 0.47,
          sLow: 0.32,
          sHigh: 0.63,
          field: "column_2100_rcp4_5"
        },
        {
          name: "RCP8.5",
          tMean: 3.7,
          tLow: 2.6,
          tHigh: 4.8,
          sMean: 0.63,
          sLow: 0.45,
          sHigh: 0.82,
          field: "column_2100_rcp8_5"
        },
        {
          name: "High End",
          tMean: 4.6,
          tLow: 2.6,
          tHigh: 4.8,
          sMean: 0.78,
          sLow: 0.45,
          sHigh: 0.82,
          field: "column_2100_high_end"
        }
      ],
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
  mounted () {
    this.$nextTick(this.pinContainerScene)
  },
  computed: {
    tempIcon() {
      const url = require('~/assets/img/temp.svg');
      return url;
    },
    seaIcon() {
      const url = require('~/assets/img/sea.svg');
      return url;
    },
    lamark() {
      const url = require('~/assets/img/new-lamark.jpg');
      return url;
    },
    activeScenarioFlood: function() {
      return this.activeScenario + "_flood";
    },
    activeScenarioErosion: function() {
      return this.activeScenario + "_erosion";
    }
    // activeScenarioData: function() {
    //   return this.scenarios.find(
    //     element => element.field === this.activeScenario
    //   );
    // }
  },
  components: {
    Card,
    Bell,
    Hist,
    ScenarioDetails,
    Graph,
    Tree,
    Map,
    Slider,
    BulmaAccordion,
    BulmaAccordionItem
  },
  methods: {
    pinContainerScene () {
      const Length = 6

      // Create a new Timeline (equivalent to new TimelineMax())
      const tl = new this.$gsap.TimelineMax()
      const animFrom = {y: '100%'};
      for (var i = 1; i < Length; i++) { // For each panel in this.panels array:
        // if (i !== 0) { // For each panel except the one whom index is 0, create the tween and add it to the tl timeline
          tl.fromTo(`section.panel-${i}`, 1.5, animFrom, {x: '0%', y: '0%', ease: Linear.easeNone})
        // }
      }

      // create scene and set its params
      this.scene = new this.$scrollmagic.Scene({
        triggerElement: '.pinContainer',
        triggerHook: 'onLeave',
        duration: `${Length * 100}%`
      })
      .setPin('.pinContainer')
      .setTween(tl)

      // Add scene to ScrollMagic controller by emiting an 'addScene' event on vm.$ksvuescr (which is our global event bus)
      this.$ksvuescr.$emit('addScene', 'pinContainerScene', this.scene)

      // TAAAAAAADAAAAAAAAAAAA
    }
  },
  destroyed () {
    // Destroy ScrollMagic when our component is removed from DOM
    this.$ksvuescr.$emit('destroy')
  }
};
</script>

<style>

  body {
    margin: 0;
  }
  .pinContainer {
    width: 100%;
    height: 100vh;
    overflow: hidden;
    position: relative;
  }
  .panel {
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left:0;
    display: flex;
    justify-content: center;
    align-items: center;
    background: white;
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

figure.image {
  margin: 0 auto;
}
</style>
