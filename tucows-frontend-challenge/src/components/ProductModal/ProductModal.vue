<template>
  <div class="modal">
    <div class="modal-container">
      <h2>{{ product.product }}</h2>
      <div class="modal-content">
        <img :src="product.image || placeholderImage" alt="Product image" />
        <div class="product-description">
          <h4>Key Features</h4>
          <ul v-html="featureList.join('')"></ul>
          <div v-if="product.description" class="product-description">
            <p>{{ product.description }}</p>
          </div>
        </div>
      </div>
      <div class="modal-button">
        <button @click="$emit('close')">Close</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";
import './ProductModal.scss';

const props = defineProps({
  product: {
    type: Object,
    required: true,
  },
});

const featureList = computed(() => {
  return props.product.features && typeof props.product.features === "object"
    ? Object.values(props.product.features).map(
        (feature) => `<li>${feature}</li>`
      )
    : ["No description available."];
});

const placeholderImage = computed(
  () => "https://via.placeholder.com/150?text=No+Image"
);
</script>