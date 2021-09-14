<template>

    <h1>Home</h1>
    
    <hr />

    <n-grid x-gap="12" :cols="4">

      <Card v-for="(list, index) in employees" :key="index" 
      :name='list.name' :role='list.role' :image='list.image' :review='list.review' />

    </n-grid>

</template>

<script lang="ts">
import { defineComponent } from 'vue'
// UI
import { NGrid } from 'naive-ui'
// components
import Card from '../components/Card.vue'
// API calls
import TutorialService from "../services/ApiRequest"
// types
import { Item, ResponseData } from "../types/ApiTypes"

export default defineComponent({
  name: 'Home',
  components: {
    Card,
    NGrid,
  },
  data(){
    return {
      employees: [] as Array<Item> 
    }
  },
  methods: {
    retrieveTutorials() {
      TutorialService.getAll()
        .then((response: ResponseData) => {
          this.employees = response.data
          console.log(response.data)
        })
        .catch((e: Error) => {
          console.log(e)
        });
    },
  },
  mounted() {
      this.retrieveTutorials()
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
