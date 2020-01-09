<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md row items-start q-gutter-md items-center">
      <q-card class="my-card">
        <img :src="frontImage">

        <q-card-section>
          <div class="text-h6 capitalize">{{ pokeName.charAt(0).toUpperCase() + pokeName.slice(1) }}</div>
          <div class="text-subtitle2">ID: {{pokemon.id}}</div>
        </q-card-section>

        <q-card-section>
          <q-list dense bordered padding class="rounded-borders">
            <q-item clickable v-ripple>
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
          <p>Abilities:</p>
          <q-list dense bordered padding class="rounded-borders">
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
    </div>

    <div class="q-pa-md">
    <q-card class="my-card">
      <q-card-section>
        <div class="text-h6">Our Changing Planet</div>
        <div class="text-subtitle2">by John Doe</div>
      </q-card-section>

      <q-markup-table>
        <thead>
          <tr>
            <th class="text-left">Dessert (100g serving)</th>
            <th class="text-right">Calories</th>
            <th class="text-right">Fat (g)</th>
            <th class="text-right">Carbs (g)</th>
            <th class="text-right">Protein (g)</th>
            <th class="text-right">Sodium (mg)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="text-left">Frozen Yogurt</td>
            <td class="text-right">159</td>
            <td class="text-right">6</td>
            <td class="text-right">24</td>
            <td class="text-right">4</td>
            <td class="text-right">87</td>
          </tr>
          <tr>
            <td class="text-left">Ice cream sandwich</td>
            <td class="text-right">237</td>
            <td class="text-right">9</td>
            <td class="text-right">37</td>
            <td class="text-right">4.3</td>
            <td class="text-right">129</td>
          </tr>
          <tr>
            <td class="text-left">Eclair</td>
            <td class="text-right">262</td>
            <td class="text-right">16</td>
            <td class="text-right">23</td>
            <td class="text-right">6</td>
            <td class="text-right">337</td>
          </tr>
          <tr>
            <td class="text-left">Cupcake</td>
            <td class="text-right">305</td>
            <td class="text-right">3.7</td>
            <td class="text-right">67</td>
            <td class="text-right">4.3</td>
            <td class="text-right">413</td>
          </tr>
          <tr>
            <td class="text-left">Gingerbread</td>
            <td class="text-right">356</td>
            <td class="text-right">16</td>
            <td class="text-right">49</td>
            <td class="text-right">3.9</td>
            <td class="text-right">327</td>
          </tr>
        </tbody>
      </q-markup-table>
    </q-card>
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
  },
  data () {
    return {
      pokemon: '',
      pokeName: '',
      frontImage: '',
      abilities: ''
    }
  }
}
</script>
