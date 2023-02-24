<template>
  <div class="row">
    <div class="col-4 offset-4 q-ma-md">
      <q-card dark bordered class="bg-grey-9 my-card">
        <q-card-section>
          <q-img v-bind:src="img" style="height: 200px; ">
            <div class="absolute-bottom text-h6">
              {{data.name}}
            </div>
          </q-img>
        </q-card-section>
        <q-separator dark inset />
        <q-card-section>
          Height : {{ data.height }}
          Weight : {{ data.weight }}
        </q-card-section>
        <q-card-section>
          <q-list>
            Types :
            <q-item clickable v-for="item in data.types" v-bind:key="item.slot">
                <q-item-section>
                  <q-item-label>{{ item.type.name }}</q-item-label>
                </q-item-section>
            </q-item>
          </q-list>
        </q-card-section>
        <q-card-section >
          <q-list>
            Abilities :
            <q-item clickable v-for="item in data.types" v-bind:key="item.slot">
                <q-item-section>
                  <q-item-label>{{ item.type.name }}</q-item-label>
                </q-item-section>
            </q-item>
          </q-list>
        </q-card-section>
        <q-separator dark />
        <q-card-actions>
          <router-link to="/"><q-btn flat class="text-white">Data Pokemon</q-btn></router-link>
        </q-card-actions>
      </q-card>
    </div>
  </div>
</template>


<script>
import { defineComponent, ref } from "vue"
import axios from "axios"
import { useRoute } from "vue-router"

export default defineComponent({
  name: 'DetailView',
  setup() {
    const data = ref([])
    const img = ref("")
    const route = useRoute()
    axios.get(`https://pokeapi.co/api/v2/pokemon/${route.params.id}`)
    .then((response) => {
      data.value = response.data
      img.value = response.data.sprites.front_default
      console.log(response)
    })
    return {
      data,
      img
    }
  }
})
</script>