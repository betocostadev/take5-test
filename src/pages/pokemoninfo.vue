<template>
  <q-page class="flex flex-center">
    <div class="q-pa-sm column items-start q-gutter-md items-center">
      <q-card class="my-card shadow-5">
        <img :src="frontImage">

        <q-card-section>
          <div class="text-h6 text-center">{{ pokeName.charAt(0).toUpperCase() + pokeName.slice(1) }}</div>
          <div class="text-subtitle2 text-center">ID: {{pokemon.id}}</div>
        </q-card-section>

        <q-card-section>
          <q-list dense bordered padding class="rounded-borders">
            <q-item v-ripple>
              <q-item-section>
                Base experience: {{pokemon.base_experience}}
              </q-item-section>
              <q-item-section>
                Height: {{pokemon.height}}
              </q-item-section>
              <q-item-section>
                Weight: {{pokemon.weight}}
              </q-item-section>
            </q-item>
          </q-list>
          <h5>Stats:</h5>
          <q-list dense padding>
            <q-item v-for="(index, stat) in stats" v-bind:key="stat">
              <q-item-section>
                <q-item-label overline>
                  {{index}}
                </q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
          <h5>Abilities:</h5>
          <q-list dense padding>
            <q-item v-for="(index, ability) in abilities" v-bind:key="ability">
              <q-item-section>
                <q-item-label overline>
                  {{index.ability.name}}
                </q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-card-section>
      </q-card>
    <div class="row">
      <q-btn to="/" color="amber" glossy label="Back" />
    </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PokemonInfo',
  async created () {
    const pokemon = await this.$axios.get(`https://pokeapi.co/api/v2/pokemon/${this.$route.params.id}`)
    console.log(pokemon.data)
    this.pokemon = pokemon.data
    this.pokeName = pokemon.data.name
    this.frontImage = pokemon.data.sprites.front_default
    this.abilities = pokemon.data.abilities
    this.stats = pokemon.data.stats.map((stat) => {
      return `Name: ${stat.stat.name}, Base: ${stat.base_stat}, Effort: ${stat.effort}`
    })
    console.log(this.stats)
  },
  data () {
    return {
      pokemon: '',
      pokeName: '',
      frontImage: '',
      abilities: '',
      stats: []
    }
  }
}
</script>
