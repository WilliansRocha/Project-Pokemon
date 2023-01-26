<script setup>
  import { onMounted, reactive, ref, computed } from 'vue';
  import ListPokemons from '../components/ListPokemons.vue'
  import CardSelected from '../components/CardSelected.vue';

  let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/") // criei uma variavel para receber o link das imagens dos pokemons, para tornar dinamico 
  let pokemons = reactive(ref());
  let searchPokemonField = ref("");
  let pokemonSelected = reactive(ref());
  let img = reactive(ref());
  let loading = ref(false)

    onMounted(() => {
      fetch("https://pokeapi.co/api/v2/pokemon?limit=1000&offset=0")
      .then(res => res.json())
      .then(res => {
       pokemons.value = res.results
      })
   
  })

  const pokemonsFiltered = computed(()=>{
    if(pokemons.value && searchPokemonField.value){
      return pokemons.value.filter(pokemon =>
      pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
      )
    }
    return pokemons.value;
  })
 
const selectPokemon = async (pokemon) => {
  loading.value = true
  await fetch(pokemon.url).then(res => res.json())
  .then(res => pokemonSelected.value = res)
  .catch(err => alert(err))
  .finally(() => loading.value = false)
  console.log(pokemonSelected.value)

}

</script>

<template>
  <main>
    <div class="container" style="display: flex">
    <!--   <div class="row-sm-12 col-md-6 mt-4" >
         <CardSelected 
         :name="pokemonSelected?.name"
         :xp="pokemonSelected?.base_experience"
         :height="pokemonSelected?.height"
         :img="pokemonSelected?.sprites.other.dream_world.front_default"
         /> -->
       <div class="mt-4 col-md-4" >
        <div class="row-sm-12 col-md-6" style="width: 100%">
         <CardSelected 
         :name="pokemonSelected?.name"
         :xp="pokemonSelected?.base_experience"
         :height="pokemonSelected?.height"
         :img="pokemonSelected?.sprites.other.dream_world.front_default"
         :loading="loading"
         
         />
      </div>  
    </div>
          <div class="col-sm-12 col-md-6 mt-4" style="margin-left: 30px">
            <div class="card card-list">
            <div class="card-body row">

              <div class="mb-3">
              <label
               hidden
               for="searchPokemonField" 
               class="form-label">
               Pesquisar...
              </label>

              <input 
              v-model="searchPokemonField"
              type="text" 
              class="form-control" 
              id="searchPokemonField" 
              placeholder="Pesquisar...">

            </div>  

            <ListPokemons v-for="pokemon in pokemonsFiltered" :key="pokemon.name" :name="pokemon.name" :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'" 
            @click="selectPokemon(pokemon)"
            />
             <!--Nessa parte eu passo atraves da props o link completo da imagem do respectivo pokemon, através da url dele, tem acesso ao seu indice, dessa maneira, acesso atraves de pokemon.url e utilizo o metodo split para dividir a url a cada barra / e na sexta divisão da url, depois da 6 barra eu pego o valor que ta la, no caso é o indice do pokemon, e adiciono a variavel criada urlBaseSvg que contem a url de acesso as imagens dos pokemons, concatenando assim a url + id do pokemon + .svg, dessa  maneira envio o link completo através do props para o componente que vai adicionar a imagem ao card-->
  
            </div>     
        </div>
    </div>
  </div>
  </main>
</template>

<style scoped>
  .card-list{
    max-height: 60vh;
    overflow-y: scroll;
    overflow-x: hidden; /** Overflow modifica a barra de rolagem, colocou barra de rolagem no eixo y ou seja na vertical e removeu a barra de rolagem no eixo x horizontal, atraves ado hidden */
  }
</style>
