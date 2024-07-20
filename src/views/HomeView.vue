<script setup>
import Heroe from '@/components/Heroe.vue';
import HomeCards from '@/components/HomeCards.vue';
import JobListings from '@/components/JobListings.vue';
</script>

<template>
  <Heroe />
  <HomeCards />
  <JobListings :limit="3" :showButton="true" />
</template>