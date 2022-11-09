<script setup>
import distance from "jaro-winkler";
import CompareIcon from "./components/icons/CompareIcon.vue";
import ClearIcon from "./components/icons/ClearIcon.vue";
import Header from "./components/Header.vue";
import Grid from "./components/Grid.vue";
</script>

<script>
export default {
  data() {
    return {
      dimestions: [10, 55],
      results: [],
      showGrid: true,
      showClear: false,
      word1: "",
      word2: "",
      score: 0,
    };
  },
  methods: {
    clear: function (event) {
      this.results = [];
      this.word1 = "";
      this.word2 = "";
      this.showClear = false;
    },
    compare: function (event) {
      var am2 = distance(this.word1, this.word2, { caseSensitive: false });
      var likely = false;
      if (am2 > 0.5) {
        likely = true;
      }
      this.results.push({
        key: this.word1,
        answer: this.word2,
        score: am2,
        likelyhood: likely,
      });
      this.showGrid = true;
      this.showClear = true;
    },
  },
};
</script>

<style>
#btnCompare {
  width: 15%;
  height: 115%;
}
</style>

<template>
  <Header />
  <main class="mt-5">
    <div class="container">
      <section>
        <div class="d-flex flex-row justify-content-around align-items-center">
          <div>
            <textarea
              :rows="this.dimestions[0]"
              :cols="this.dimestions[1]"
              style="resize: none"
              v-model="word1"
            ></textarea>
          </div>
          <div>
            <textarea
              :rows="this.dimestions[0]"
              :cols="this.dimestions[1]"
              v-model="word2"
              style="resize: none"
            ></textarea>
          </div>
        </div>
      </section>
    </div>

    <div class="container text-center">
      <button @click="compare" class="btn btn-info mx-1">
        <CompareIcon width="30" /> Compare
      </button>
      <button @click="clear" v-if="showClear" class="btn btn-danger mx-1">
        <ClearIcon width="30" /> Clear
      </button>
    </div>
    <Grid :results="results" :showGrid="showGrid" />
  </main>
</template>
