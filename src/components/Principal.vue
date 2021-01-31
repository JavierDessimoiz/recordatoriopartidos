<template>
  <div class="container">
    <h1>{{ msg }}</h1>
    
      <div class="container">

          <div
            class="row"
            v-for="match in todayMatches.matches"
            :key="match.id"
          >
            <div class="col">
              {{ match.homeTeam.name }}
            </div>
            <div class="col">
              vs
            </div>
            <div class="col">
              {{ match.awayTeam.name }}
            </div>
            <div class="col">
              {{ match.competition.name }}
            </div>
          </div>
        </div>
      </div>

</template>

<script>
import axios from "axios";

export default {
  name: "principal",
  props: {
    msg: String
  },
  data() {
    return {
      todayMatches: null
    };
  },
  mounted() {
    this.gettodayMatches();
  },
  methods: {
    gettodayMatches() {
      axios
        .get("https://api.football-data.org/v2/matches", {
          headers: { "X-Auth-Token": "43baecc6037a4fdba4aa8dc9e4f2e36e" }
        })
        .then(response => {
          this.todayMatches = response.data;
        })
        .catch(e => console.log(e));
    },
  }
};
</script>

<style scoped>
.col {
  border: 1px solid black
}
</style>
