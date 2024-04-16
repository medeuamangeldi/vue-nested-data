<template>
  <tr @click="toggleCollapse" v-if="item">
    <td v-bind:style="{ paddingLeft: `${paddingLeft}px` }">
      <span
        v-bind:style="{ fontSize: '12px', width: '100%', padding: '10px' }"
        >{{ expanded ? "🔽" : "🔼" }}</span
      >{{ name }}
    </td>
    <td v-for="year in years">
      {{ numberWithSpaces(item.data[year.value]) || "-" }}
    </td>
  </tr>
  <HierarchyItem
    v-if="expanded"
    v-for="(child, key) in item.children"
    :name="key"
    :item="child"
    :years="years"
    :paddingLeft="paddingLeft + 10"
  />
</template>

<script>
export default {
  props: ["item", "years", "name", "paddingLeft", "icon"],
  data() {
    return {
      expanded: false,
    };
  },
  methods: {
    toggleCollapse() {
      this.expanded = !this.expanded;
    },
    numberWithSpaces(x) {
      return x?.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ");
    },
  },
};
</script>

<style scoped>
td {
  padding: 10px;
  border: 1px solid black;
}
</style>
