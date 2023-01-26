<script setup>
  import {ref,reactive ,onMounted, computed} from 'vue'
    let nome = ref('Vue');

    onMounted(() => {
      nome.value = 'Vite'
    })

    let temperatura = ref(22)
    const verificaTemperatura = computed(() => {
      return temperatura.value > 21 ? 'Temperatura alta' : 'Temperatura baixa'
    })

    let person = reactive({
      name: 'Joe',
      age: 30
    })

    onMounted(() => {
      person.name = 'John'
      nome.value = 'Teste'
      console.log(person)
    })
    
</script>

<template>
  <div class="col-6">
    <h2>Composition</h2>
    <p>{{ nome }}</p>
    <input type="text" v-model="nome">
    <hr>
  <input type="text" v-model="temperatura">
  <br>
    <span>{{ verificaTemperatura }}</span>

    <br>
    <p>{{ person.name }}</p>
    <p>{{ person.age }}</p>
    <p>{{ nome }}</p>
  </div>
  
</template>

<style scoped>

</style>
