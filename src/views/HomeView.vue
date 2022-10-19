<style scoped>
@import '../assets/styles/main.css';
</style> 
<template>
  <main>
    <div v-for="i in countries" v-bind:key="i" class="country">
      <router-link :to="{ path: '/detail/' + i.cca3}">
        <article>
          <center><img :src="i.flags.png" /></center>
          <center>
            <h2>{{i.translations.pol.official}}</h2>
          </center>
          <center style="margin-bottom: 20px;">{{i.name.official}}</center>
          <div style="display: none;">
            <center>
              Population: {{i.population}}
            </center>
          </div>
        </article>
      </router-link>
    </div>
  </main>
  <router-view></router-view>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  name: 'HomeView',
  data() {
    return {
      countries: [] as Array<any>,
    }
  },
  methods: {
    getCountries() {
      axios.get("https://restcountries.com/v3.1/all").then((res: any) => {
        this.countries = res.data
        res.data.forEach((element: any) => {
          console.log(element)
        });
      })
    },
    showMore(event: any) {
      let target = event.target
      console.log(target)
    }
  },
  mounted() {
    this.getCountries()
  }
});
</script>