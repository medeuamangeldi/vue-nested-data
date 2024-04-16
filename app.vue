<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>Наименование</th>
          <th v-for="year in years">{{ year.label }}</th>
        </tr>
      </thead>
      <tbody>
        <HierarchyItem
          v-for="(item, key) in jsonData"
          :name="key"
          :item="item"
          :years="years"  
          :paddingLeft="0"
          :icon="expanded ? '🔽' : '🔼'"
        />
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import HierarchyItem from "@/components/HierarchyItem.vue";

export default {
  data() {
    return {
      years: [
        { value: 2020, label: "Год 2020" },
        { value: 2021, label: "Год 2021" },
        { value: 2022, label: "Год 2022" },
        { value: 2023, label: "Год 2023" },
        { value: 2024, label: "Год 2024" },
      ],
      jsonData: null,
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios
          .get("res-second-task.json")
          .then((res) => res.data);
        this.jsonData = response;
      } catch (error) {
        console.error("Error fetching JSON data:", error);
      }
    },
  },
};
</script>

<style scoped>
table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
}

table {
  width: 100%;
}

th {
  padding: 20px;
}
</style>
