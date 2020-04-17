<template>
  <b-row>
    <b-col md="6">
      <p v-if="job.owner">{{job.owner.username}}</p>
      <h2>{{job.title}}</h2>
      <p>{{job.fulltime ? 'Full-time' : 'Part-time'}} / {{job.location}}</p>
      <b-badge v-if="job.category">{{job.category}}</b-badge>
    </b-col>
    <b-col md="6" class="d-flex justify-content-around align-items-center">
      <span>
        <small>posted</small>
        <h4>{{formatDate(job.created_at)}}</h4>
      </span>
      <span>
        <h4>{{daysAgo(job.created_at)}} ago</h4>
      </span>
    </b-col>
  </b-row>
</template>

<script>
import { format, formatDistance } from "date-fns";
export default {
  name: "JobData",
  props: { job: { type: Object, required: true } },
  methods: {
    formatDate(date) {
      return format(Date.parse(date), "do MMM");
    },
    daysAgo(date) {
      return formatDistance(Date.parse(date), new Date());
    }
  }
};
</script>

<style scoped>
</style>

