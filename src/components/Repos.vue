
<template>
  <b-container>
    <Row v-for="repo in repos" v-bind:key="repo.id" v-bind:repo="repo" />
    <Observer v-on:intersect="load_more" />
  </b-container>
</template>

<script>
// ROW MODEL LOOK AT COMPENENT FOLDER
import Row from "./Row";
// IMPORT OBSERVER TO SEE IF WE REACH THE END OF THE PAGE
import Observer from "./Observer";
// MOMENT: JUST TO GET THE DATE 30 DAYS AGO
var moment = require("moment");

export default {
  name: "Repos",
  data() {
    return {
      repos: [],
      page: 1,
      lastDate: moment()
        .add(-30, "days")
        .format("YYYY-MM-DD")
    };
  },
  methods: {
    async load_more() {
      // WAIT FOR DATA TO CPME FROM GITHUB API
      const res = await fetch(
        `https://api.github.com/search/repositories?q=created:>${
          this.lastDate
        }&sort=stars&order=desc&page=${this.page++}`
      );
      // PARSE GITHUB API RES
      const data = await res.json();
      // CHECK IS THE DATA IS ENDED OR NOT
      if (data && data.items && data.items.length) {
        const repos = data.items;
        // MERGE THE NEW RESULT (REPOS) TO THE OLD ONES
        this.repos = [...this.repos, ...repos];
      }
    }
  },
  components: {
    Row,
    Observer
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>