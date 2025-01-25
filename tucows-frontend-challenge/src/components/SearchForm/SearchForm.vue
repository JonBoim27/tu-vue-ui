<template>
  <header>
  <div class="logo-container">
    <img
      class="storm-icon"
      src="../../assets/img/storm-icon.png"
      alt="Storm Icon"
    />
    <img src="../../assets/img/storm-logo3.svg" alt="Storm Logo" />
  </div>
  <div class="search-container">
    <form class="search-form" @submit.prevent="handleClick">
      <input
        type="text"
        id="search"
        v-model="inputValue"
        placeholder="Search"
        class="search-bar"
      />
      <button type="submit">Search</button>
    </form>
  </div>
  <div class="icons-container">
    <img src="../../assets/img/gear-icon.svg" alt="gear icon" />
    <img src="../../assets/img/notifications.png" alt="bell icon" />
    <img src="../../assets/img/profile-icon.png" alt="profile icon" />
    <div class="profile-name">Adriana Arias</div>
  </div>
</header>
</template>

<script setup>
import { ref, defineEmits } from "vue";
import './SearchForm.scss';

const inputValue = ref("");
const emit = defineEmits(["searchButtonClick"]);
const handleClick = () => {
  emit("searchButtonClick", inputValue.value);
};

</script>

<style lang="scss"></style>
