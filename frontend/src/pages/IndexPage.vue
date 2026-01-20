<template>
  <q-page padding>
    <div class="text-h5 q-mb-md">Frontend Axios Demo</div>

    <div v-if="loading">Loading...</div>
    <pre v-else>{{ data }}</pre>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const loading = ref(true)
const data = ref(null)

const fetchData = async () => {
  loading.value = true
  const url = import.meta.env.VITE_API_URL + '/api/demo'
  const res = await axios.get(url)
  data.value = res.data
  loading.value = false
}

onMounted(fetchData)
</script>
