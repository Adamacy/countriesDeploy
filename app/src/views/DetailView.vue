<template>
    <div id="detail">
        <nav>
            <img :src="data.flags.png" /><br>
            <center>
                <h1>{{data.name}}</h1>
            </center>
            <center>
                <h2>{{data.nativeName}}</h2>
            </center>
            <center>
                <h3>{{data.alpha2Code}} / {{data.alpha3Code}}</h3>
            </center>
            <center>
                <p>Stolica: {{data.capital}}</p>
            </center>
            <center>Kontynent: {{data.region }}</center>
        </nav>
        <section>
            <p>Populacja: {{data.population}}</p>
            <p>Powierzchnia: {{ data.area }} km&#178;</p>
            <p v-for="language in data.languages" v-bind:key="(language as any)">Język: {{language.name }}</p>
            Sąsiedzi: <p v-for="border in data.borders" v-bind:key="border">
                <a :href="'/detail/' + border">{{ border }}</a>
            </p>
            <p>Telefoniczny kod kraju: + {{ data.callingCodes[0] }}</p>
            <p>Niezależny: {{data.independent ? "Tak" : "Nie"}}</p>
            <p v-for="domain in data.topLevelDomain" v-bind:key="domain">Domena: {{ data.name }} <b>{{ domain }}</b></p>
        </section>

    </div>image.png

</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';
import { ElementTypes } from '@vue/compiler-core';

export default defineComponent({
    name: "DetailView",
    data() {
        return {
            data: {
                capital: '',
                population: 2137,
                name: 'Jan Pat 2',
                nativeName: "Ped****",
                alpha2Code: 'JP',
                alpha3Code: 'JP2',
                flags: {
                    png: require("../assets/images/pat.png")
                },
                area: 420,
                borders: [],
                timezones: ["UTC+02:00"],
                languages: [
                    { name: 'Watykański' },
                ],
                callingCodes: [],
                region: '',
                currencies: [
                    { name: '' }
                ],
                independent: true,
                topLevelDomain: ['.jp'],
            },

        }
    },
    methods: {
        getCountry() {
            let cca3 = this.$route.params.cca3
            axios.get("https://restcountries.com/v2/all").then((res: any) => {
                res.data.forEach((element: any) => {
                    if (element.alpha3Code == cca3) {
                        this.data = element
                        console.log(element)
                    }
                });
            })
        },
    },
    mounted() {
        this.getCountry();
    }
})
</script>