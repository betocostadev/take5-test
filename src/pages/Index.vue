<template>
  <q-page class="flex flex-center">
    <h2>Pokedex</h2>
    <button v-on:click="loadData()">Show</button>
    <button v-on:click="say(loadData())">Show2</button>
    <ul id="example-1">
      <li v-for="pokemon in pokemons" v-bind:key="pokemon.name">
        {{ pokemon.name }}
      </li>
    </ul>
  </q-page>
</template>

<script>

/* Colocando os dados como Pokemon e retornando está funcionando. Talvez o melhor seja:
Carregar os dados usando o "mounted". Usar um botão que irá colocar tudo na página, chamando os dados
que já estarão carregados através do mounted. */

import { date } from 'quasar'
export default {
  name: 'PageIndex',
  methods: {
    say: function (msg) {
      alert(msg)
    },
    loadData () {
      const test = this.$axios.get('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=40')
        .then((response) => {
          const data = response.data.results
          // this.data = response.data
          console.log(data)
        })
      return test
    }
  },
  computed: {
    todaysDate () {
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'YYYY-MM-DD')
    }
  },
  mounted () {
    this.$nextTick(function () {
      const pokemons = this.$axios.get('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=40')
        .then((response) => {
          const data = response.data.results
          return data
        })
      return pokemons
    })
  }
}
</script>
