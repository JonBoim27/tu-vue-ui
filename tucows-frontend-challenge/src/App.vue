<template>
  <div class="header">
    <div class="table-container">
       <DataTable :items="items" />
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import DataTable from './components/DataTable/DataTable.vue';
import jsonData from './assets/mockData/products.json';
const items = ref([]);

const fetchProducts = async () => {
      try {
        console.log("Fetching products...");
        const response = await Promise.resolve({ data: jsonData });
        if (!response?.data) {
          throw new Error(`Failed to fetch products: ${response.statusText}`);
        }
         items.value = response?.data;
      } catch (error) {
        console.error("Error fetching products:", error);
      }
    };

onMounted(fetchProducts);
</script>
