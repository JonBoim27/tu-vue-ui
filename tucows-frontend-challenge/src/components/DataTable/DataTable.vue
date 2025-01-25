<template>
  <div>
    <div>
      <SearchForm @searchButtonClick="handleSearch" />
    </div>
    <div class="show-products-container">
      <p>
        <span class="bold-text">Products</span> {{ filteredAndSortedProducts.length }} of
        {{ items.length }}
        results
      </p>
    </div>
    <table>
      <thead>
        <tr>
          <th @click="sortBy('id')">ID</th>
          <th>Status</th>
          <th @click="sortBy('quantity')">Quantity</th>
          <th @click="sortBy('product')">Product name</th>
          <th @click="sortBy('total')">Price</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in filteredAndSortedProducts"
          :key="item?.id"
          @click="selectProduct(item)"
        >
          <td>{{ item?.id }}</td>
          <td class="status-container">
            <StatusLabel :status="status" />
          </td>
          <td>{{ item?.quantity }}</td>
          <td>
            <div>
              <div>{{ item?.product }}</div>
              <div class="serial-container">{{ item?.serial }}</div>
            </div>
          </td>
          <td>${{ item?.total?.toFixed(2) }}</td>
        </tr>
      </tbody>
    </table>

    <ProductModal
      v-if="selectedProduct"
      :product="selectedProduct"
      @close="selectedProduct = null"
    />
  </div>
</template>

<script setup>
import { computed, ref, watch } from "vue";
import SearchForm from "../SearchForm/SearchForm.vue";
import ProductModal from "../ProductModal/ProductModal.vue";
import StatusLabel from "../StatusLabel/StatusLabel.vue";

const selectedProduct = ref(null);
const searchFilter = ref("");
const sortKey = ref("");
const sortOrder = ref(1);
const isItemsPopulated = ref(false);

const props = defineProps({
  items: {
    type: Array,
    required: true,
  },
  status : {
    type: String,
    default: 'Status'
  }
});

watch(() => props.items, (newItems) => {
  if (newItems && newItems.length > 0) {
    isItemsPopulated.value = true;
  }
});

const filteredAndSortedProducts = computed(() => {
  if (!isItemsPopulated.value) return [];
      const filtered = props?.items?.filter((product) =>{
        return product.product.toLowerCase().includes(searchFilter.value.toLowerCase())
      }
      );
      if (!sortKey.value) return filtered;
      return filtered.sort((a, b) => {
        const valueA = a[sortKey.value];
        const valueB = b[sortKey.value];
        return (valueA > valueB ? 1 : -1) * sortOrder.value;
      });
    });

const sortBy = (key) => {
  if (sortKey.value === key) {
    sortOrder.value *= -1;
  } else {
    sortKey.value = key;
    sortOrder.value = 1;
  }
};

const selectProduct = (product) => {
  selectedProduct.value = product;
};

const handleSearch = (search) => {
  searchFilter.value = search;
  console.log(search);
};
</script>
