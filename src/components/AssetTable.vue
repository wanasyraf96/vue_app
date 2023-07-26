<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  setup() {
    const assets = [
      { assets_name: "Printer", department: "HR" },
      { assets_name: "Monitor", department: "IT" },
      { assets_name: "Barcode Scanner", department: "ACCOUNT" },
    ];
    return { assets };
  },
  methods: {
    downloadCSV() {
      const data = this.assets;
      const headers = Object.keys(data[0]).join(",") + "\n";

      const rows = data.map((item) =>
        Object.values(item)
          .map((value) => `${value}`)
          .join(",")
      );

      const csvString = headers + rows.join("\n");

      // downloadable CSV link
      const blob = new Blob([csvString], { type: "text/csv" });
      const url = window.URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href = url;
      a.download = "data.csv";
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      window.URL.revokeObjectURL(url);
    },
  },
  // props: {
  //   data: {
  //     type: [Array, Object],
  //   },
  // },
  // data() {
  //   console.log(this.data);
  //   return { assets: this.data };
  // },
});
</script>

<template>
  <div class="asset-table">
    <table>
      <thead>
        <tr>
          <th class="th">Asset Name</th>
          <th class="th">Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(asset, index) in assets" :key="index">
          <td>{{ asset.assets_name }}</td>
          <td>{{ asset.department }}</td>
        </tr>
      </tbody>
    </table>
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>

<style scoped>
.asset-table {
  margin: 20px auto;
  max-width: 700px;
  font-family: Arial, Helvetica, sans-serif;
  position: relative;
}
button {
  margin: 10px 0;
  width: 100%;
  background-color: #007bff;
}
table {
  width: 100%;
  border-collapse: collapse;
  border: 1px solid #ddd;
}
th,
td {
  padding: 10px;
  text-align: left;
}

th {
  background-color: #555;
  color: white;
}

tr:nth-child(even) {
  background-color: #999;
}

tr:hover {
  background-color: #aaa;
}
</style>