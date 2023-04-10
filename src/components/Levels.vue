<template>
  <div v-for="(n, index) in sortedLevels" :class="{ active: index == lIndex }">
    {{ n }}
  </div>
</template>

<script>
export default {
  props: ["levels", "lIndex"],
  data() {
    return {};
  },
  computed: {
    sortedLevels() {
      return this.levels.sort((a, b) => b - a);
    },
  },
};
</script>
