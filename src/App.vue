<script setup>
import {ref} from "vue";
import DefaultLayout from "./layouts/DefaultLayout.vue";
import Customers from "./pages/Customers.vue";
import Start from "./pages/Start.vue";

const activeTab = ref(0);

const setActive = (active) => {
  activeTab.value = active;
}
</script>

<template>
  <DefaultLayout :menuToggle="setActive" :currentTab="activeTab">
    <Start v-if="activeTab === 0"/>
    <Customers v-if="activeTab === 1"/>
  </DefaultLayout>
</template>

<style scoped>

</style>
