<template>
  <p class="filter">{{ filterText }}</p>
</template>

<script>
export default {
  name: "Filter",
  props: {
    filterText: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
.filter {
  font-weight: 700;
  color: #5ba4a4;
  background: #eef6f6;
  
  cursor: pointer;
  border-radius: 5px;
  padding: 1rem 1.5rem;  
  transition: all 0.2s ease-out;
}
</style>