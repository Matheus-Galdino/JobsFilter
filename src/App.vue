<template>
  <header></header>

  <main>
    <ActiveFilters
      :filters="filters"
      v-show="filters.length > 0"
      @removeFilter="removeFilter($event)"
      @clearFilters="filters.length = 0"
    />

    <section class="jobs">
      <Job
        :job="job"
        v-for="job in filteredJobs"
        :key="job.id"
        @addFilter="addFilter($event)"
      />
    </section>
  </main>

  <!-- <div class="attribution">
    Challenge by <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>.
    Coded by <a href="#">Your Name Here</a>.
  </div> -->
</template>

<script>
import Job from "./components/Job";
import ActiveFilters from "./components/ActiveFilters";

export default {
  name: "App",
  components: {
    Job,
    ActiveFilters,
  },
  data() {
    return {
      jobs: [],
      filters: [],
    };
  },
  methods: {
    addFilter(filter) {
      if (this.filters.some((x) => x === filter)) return;

      this.filters.push(filter);
    },
    removeFilter(filter) {
      const index = this.filters.indexOf(filter);

      this.filters.splice(index, 1);
    },
  },
  computed: {
    filteredJobs() {
      if (this.filters.length == 0) return this.jobs;

      const filteredJobs = [];
      this.jobs.forEach((job) => {
        const jobFilters = [
          job.role,
          job.level,
          ...job.languages,
          ...job.tools,
        ];

        if (this.filters.every((val) => jobFilters.includes(val)))
          filteredJobs.push(job);
      });

      return filteredJobs;
    },
  },
  beforeMount() {
    this.jobs = require("./data.json");
  },
};
</script>

<style lang="scss">
@import "./style/variables.scss";

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

header {
  height: 15vh;
  background: $darkCyan url("./assets/bg-header-mobile.svg") no-repeat;
  background-size: cover;
}

main {
  min-height: 85vh;

  padding: 1rem 3rem 4rem;
  background: $lightCyanBg;
}

.jobs {
  margin-top: 3rem;
}

@media (min-width: 1440px) {
  main {
    padding: 1rem 300px 4rem;
  }
}
</style>
