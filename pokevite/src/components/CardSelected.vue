
<script setup>
    const pokemon= defineProps(["name", "xp", "height", "img", "loading"])
</script>
<template>
        <div class="card cardPokemonSelected " 
        :class=" loading ?'' : 'animate__animated animate__zoomIn'">
        <img :src="pokemon.img" class="card-img-top pt-2" alt=""
        height="250"
        >
        <div class="card-body">
          <h5 class="card-title text-center" style="text-transform:uppercase">{{ pokemon.name }}</h5>
          <hr>

          <div class="row">
            <section class="col">
              <strong>Xp:</strong>
              <span class="info">{{ pokemon.xp }}</span>
            </section>
            <section class="col">
              <strong>Altura:</strong>
              <span class="info">{{pokemon.height}}</span>
            </section>
          </div>
        </div>
        </div>
</template>


<style scoped>

 .info{
    margin-left: 5px;
    font: bolder;
  }
  .cardPokemonSelected{
    height: 40vh;
    background: rgb(131,58,180);
    background: radial-gradient(circle, rgba(131,58,180,1) 0%, rgba(253,29,29,1) 50%, rgba(252,176,69,1) 100%);
  }
</style>

