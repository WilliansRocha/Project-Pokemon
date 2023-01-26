<script setup>
const pokemon = defineProps(["name", "urlBaseSvg"])

</script>

<template>
    <div class="col-4">
        <div class="card p-2 mb-3 cardListPokemon" >
           <p class="text-center" >{{pokemon.name}}</p>
            <img :src="urlBaseSvg" class="card-img-top" alt="..." height="80"> 
        </div>
    </div>
</template>

<style scoped>
    .cardListPokemon{
        background: rgb(2,0,36);
        background: radial-gradient(circle, rgba(2,0,36,1) 0%, rgba(9,9,121,0.53824362606) 0%, rgba(0,212,255,0.5) 100%);
        cursor: pointer;
    
}
.cardListPokemon img{
    padding: 0.2em;
}
.cardListPokemon:hover{
        background: rgb(2,0,36);
        background: radial-gradient(circle, rgba(2,0,36,1) 0%, rgba(9,9,121,0.7) 0%, rgba(0,212,255,0.7) 100%);
}
.cardListPokemon img:hover{
    padding: 0px;
}

p{
    
    color: white;
    text-transform: uppercase;
    font: bold;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-size: 12px;
}

</style>>

