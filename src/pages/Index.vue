<template>
  <q-page>
    <div class="column">
      <h3 class="text-h3 text-center">Pokémon list</h3>
    </div>
    <!-- <button v-on:click="loadData()">Show</button> -->
    <div class="column q-pa-md items-center">
      <div class="q-gutter-md" style="max-width: 500px">
        <q-input outlined v-model="search" label="Search" />
      </div>
    </div>

    <div class="column justify-center items-center">
      <q-list bordered separator>
        <q-item clickable v-ripple v-for="(index, pokemon) in filteredPokemons"
            v-bind:key="pokemon.url">
          <q-item-section>
            <q-item-label overline>
              {{index.url.slice(33).replace('/', '').replace('/', '')}} | {{ index.name.toUpperCase() }}</q-item-label>
            <router-link :to="{name: 'pokemoninfo', params: {id: index.name }}">Go to Info</router-link>
          </q-item-section>
        </q-item>
      </q-list>
    </div>
  </q-page>
</template>

<script>

export default {
  name: 'PageIndex',
  async created () {
    const pokemons = await this.$axios.get(`https://pokeapi.co/api/v2/pokemon/?offset=0&limit=151`)
    // console.log('pokemons are:', pokemons.data)
    this.pokemons = pokemons.data.results
  },
  data () {
    return {
      pokemons: [],
      pokemonName: '',
      search: ''
    }
  },
  computed: {
    filteredPokemons () {
      return this.pokemons.filter((pokemon) => {
        return pokemon.name.match(this.search.toLowerCase())
      })
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
}
</script>
