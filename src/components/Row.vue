<template>
  <b-row>
    <b-card class="mb-3 card">
      <b-row no-gutters>
        <b-col md="6">
          <b-card-img v-bind:src="repo.owner.avatar_url" class="rounded-0 row-avatar"></b-card-img>
        </b-col>
        <b-col md="6">
          <b-card-body v-bind:title="repo.full_name">
            <b-card-text class="description">{{repo.description}}</b-card-text>
            <b-badge variant="primary" class="ml-2">
              <b-icon-star-fill />
              STARS {{repo.stargazers_count}}
            </b-badge>
            <b-badge variant="danger" class="ml-2">
              <b-icon-alert-octagon-fill />
              {{repo.open_issues_count}}
            </b-badge>
          </b-card-body>
        </b-col>
      </b-row>
      <template v-slot:footer>
        <small class="text-muted text-center">{{fromNow(repo.created_at)}} by {{repo.owner.login}}</small>
      </template>
    </b-card>
  </b-row>
</template>

<script>
// MEMENT HERE JUST TO GET DATE FROM CREATED TIME
var moment = require("moment");

export default {
  name: "Row",
  methods: {
    fromNow(date) {
      return moment(date).fromNow();
    }
  },
  props: {
    repo: Object
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
  width: 100%;
}
.row-avatar {
  height: 200px;
  width: 200px;
}
</style>