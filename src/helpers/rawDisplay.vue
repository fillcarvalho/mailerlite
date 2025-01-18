
<template>
    <div>
      <h3>{{ title }}</h3>
      <pre class="bg-gray-300 rounded-lg p-5">{{ value }} </pre>
      <pre v-for="(ref, index) in refs" :key="index" class="bg-gray-300 rounded-lg p-5">{{ ref }} </pre>
    </div>
  </template>
  <script setup>
  import {defineProps} from 'vue';
  defineProps(['title', 'value', 'refs'])
  </script>
  <style scoped>
  pre {
    font-size: 10px;
    text-align: start;
  }
  </style>
  