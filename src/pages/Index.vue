<template>
  <q-page class="flex flex-center no-wrap">
    <h2 class="text-h2">Pokedex</h2>
    <button v-on:click="loadData()">Show</button>
    <div class="row">
    <p class="text-center">Pokémon list</p>
    <ul id="example-1">
      <li v-for="(index, pokemon) in pokemons" v-bind:key="pokemon.url">
        {{ index.name }} {{ index.url }}
      </li>
    </ul>
    </div>
  </q-page>
</template>

<script>

/* Colocando os dados como Pokemon e retornando está funcionando. Talvez o melhor seja:
Carregar os dados usando o "mounted". Usar um botão que irá colocar tudo na página, chamando os dados
que já estarão carregados através do mounted. */

export default {
  name: 'PageIndex',
  async created () {
    const pokemons = await this.$axios.get(`https://pokeapi.co/api/v2/pokemon/?offset=0&limit=40`)
    console.log('pokemons are:', pokemons.data)
    console.log('first poke:', pokemons.data.results[0])
    pokemons.data.results.forEach(pokemon => {
      console.log(pokemon.name)
    })
    this.pokemons = pokemons.data.results
  },
  data () {
    return {
      pokemons: []
    }
  },
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
  }
  // mounted () {
  //   this.$nextTick(function () {
  //     const pokemons = this.$axios.get('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=40')
  //       .then((response) => {
  //         const data = response.data.results
  //         return data
  //       })
  //     return pokemons
  //   })
  // }
}
</script>
