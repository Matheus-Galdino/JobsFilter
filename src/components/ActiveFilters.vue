<template>
  <section class="filters-container" v-show="filters.length > 0">
    <div class="filters">
      <div v-for="filter in filters" :key="filter">
        <Filter :filterText="filter" />
        <button @click="$emit('removeFilter', filter)">X</button>
      </div>
    </div>
    <button @click="$emit('clearFilters')">Clear</button>
  </section>
</template>

<script>
import Filter from "./Filter.vue";
export default {
  components: { Filter },
  name: "ActiveFilters",
  props: {
    filters: { type: Array, required: true },
  },
};
</script>

<style scoped lang="scss">
@import "../style/variables.scss";

.filters-container {
  display: flex;
  align-items: center;
  background: #fff;

  padding: 1.5rem 3rem;
  border-radius: 10px;

  box-shadow: $box-shadow;
  transform: translateY(-20px);

  .filters {
    display: flex;
    flex-wrap: wrap;
    gap: 2rem;
    flex: 1;

    div {
      padding: 0;
      display: flex;
      align-items: center;      

      .filter {
        font-size: 1.4rem;
      }

      button {
        font-size: 1.3rem;
        padding: 0.5rem;

        color: #fff;
        background: $darkCyan;

        border: none;
        height: 100%;
        border-top-right-radius: 5px;
        border-bottom-right-radius: 5px;
        
        transition: all 0.2s ease-out;

        &:hover {
          background-color: $xDarkGrayCyan;
        }
      }
    }
  }

  > button {
    border: none;
    font-weight: 700;
    color: $darkCyan;
    background: transparent;

    &:hover {
      text-decoration: underline;
    }
  }
}
</style>