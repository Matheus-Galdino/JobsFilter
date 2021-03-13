<template>
  <div :class="['job', { featured: job.featured }]">
    <div class="job__description">
      <img :src="getImage" :alt="job.company" />

      <div class="job__description__info">
        <div>
          <h2>{{ job.company }}</h2>
          <span class="new" v-show="job.new">new!</span>
          <span class="featured" v-show="job.featured">featured</span>
        </div>

        <p>{{ job.position }}</p>

        <small>
          {{ `${job.postedAt} &sdot; ${job.contract} &sdot; ${job.location}` }}
        </small>
      </div>
    </div>

    <div class="stroke"></div>

    <div class="job__filters">
      <Filter :filterText="job.role" @click="$emit('addFilter', job.role)" />
      <Filter :filterText="job.level" @click="$emit('addFilter', job.level)" />

      <Filter
        :filterText="tool"
        v-for="tool in job.tools"
        :key="tool"
        @click="$emit('addFilter', tool)"
      />

      <Filter
        :filterText="lang"
        v-for="lang in job.languages"
        :key="lang"
        @click="$emit('addFilter', lang)"
      />
    </div>
  </div>
</template>

<script>
import Filter from "./Filter";

export default {
  name: "Job",
  components: {
    Filter,
  },
  props: {
    job: {
      type: Object,
      required: true,
    },
  },
  computed: {
    getImage() {
      return require(`../assets/${this.job.logo}`);
    },
  },
};
</script>

<style scoped lang="scss">
@import "../style/variables.scss";

.job {
  position: relative;
  background: #fff;
  border-radius: 15px;

  margin-bottom: 4rem;
  padding: 5rem 3rem 2rem;

  box-shadow: $box-shadow;

  &:last-child {
    margin-bottom: 0;
  }

  &.featured::before {
    content: "";
    top: 0;
    left: 0;
    bottom: 0;
    position: absolute;

    width: 7px;
    background: $darkCyan;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
  }

  &__description {
    img {
      position: absolute;
      top: 0px;
      left: 25px;
      transform: translateY(-50%);

      width: 50px;
      height: 50px;
    }

    &__info {
      div {
        display: flex;
        align-items: center;

        h2 {
          color: $darkCyan;
          margin-right: 2rem;
        }

        span {
          display: block;
          font-size: 1.2rem;
          font-weight: 700;

          color: #fff;
          padding: 0.8rem 1rem;
          border-radius: 9999px;
          text-transform: uppercase;
        }

        .new {
          margin-right: 1rem;
          background: $darkCyan;
        }

        .featured {
          background: $xDarkGrayCyan;
        }
      }

      p {
        cursor: pointer;
        margin: 1.5rem 0;

        font-weight: 700;
        font-size: 1.8rem;

        color: $xDarkGrayCyan;
        transition: all 0.2s ease-out;

        &:hover {
          color: $darkCyan;
        }
      }

      small {
        color: $darkGrayCyan;
      }
    }
  }

  .stroke {
    width: 100%;
    height: 1px;
    background: lightgray;
    margin: 2rem 0;
  }

  &__filters {
    display: flex;
    gap: 2rem;
    flex-wrap: wrap;

    .filter {
      &:hover {
        background: $darkCyan;
        color: $lightCyanFilters;
      }
    }
  }
}

@media (min-width: 1440px) { 
  .job {
    display: flex;
    align-items: center;
    justify-content: space-between;

    padding: 3rem;
    margin-bottom: 3rem;

    &__description {
      display: flex;
      column-gap: 2rem;
      align-items: center;

      img {
        position: initial;
        transform: none;
        width: 80px;
        height: 80px;
      }
    }

    .stroke {
      display: none;
    }
  }
}
</style>
