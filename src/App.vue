<script lang="ts">
import AssetTable from "./components/AssetTable.vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
  components: {
    AssetTable,
  },
  // data() {
  //   const data: Ref<any[]> = ref([]);
  //   return { data };
  // },
  // created() {
  //   this.getData();
  // },
  // methods: {
  //   getData() {
  //     fetch("/api/data.json")
  //       .then((res) => res.json())
  //       .then((json) => {
  //         this.data = json.assets;
  //       })
  //       .catch((err) => console.error(err));
  //   },
  // },
});
</script>


<template>
  <div>
    <AssetTable />
  </div>
</template>
