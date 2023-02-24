<template>
  <q-page class="flex flex-center">
    <q-table 
      title="Data Pokemon"
      color="secondary"
      :loading="isLoading"
      :rows="data.map((item, index)=>data.value = {...item, index: index + 1})"
      :columns="columns"
    />
  </q-page>
</template>

<script>
// @ is an alias to /src

import { defineComponent, ref } from "vue"
import axios from "axios"

export default defineComponent({
  name: 'HomeView',
  setup() {
    const isLoading = ref(true)
    const data = ref([])
    const columns = [
      { name: "no", field: "index", label: "No", align: "left"},
      { name: "name", field: "name", label: "Name", align: "center", format: ((row, val) => `${val.name}`)},
      { name: "detail", field: "index", label: "Detail", align: "left", format: ((index) => <a href={`detail/${index}`} class="text-white bg-secondary q-pa-sm shadow-1" style={{borderRadius: "5px"}}>Detail</a>)},
    ]
    axios.get(`https://pokeapi.co/api/v2/pokemon/?limit=20&offset=20`)
    .then((response) => {
      data.value = response.data.results
    })
    .finally(() => {
      isLoading.value = false
    })
    return {
      isLoading,
      data,
      columns
    }
  }
})
</script>
