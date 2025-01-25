<template>
    <div class="status-label">
      <span class="status-label__text">{{ statusText }}</span>
    </div>
</template>

<script setup>

import { ref } from 'vue';
import './StatusLabel.scss';

const statusText = ref('Status');

</script>