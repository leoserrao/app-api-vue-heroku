<template>
  <div class="container grid-lg my-2 py-2 text-dark">
    <h1>Consumindo API de Cotações de Moedas</h1>
    <div class="card">
      <div class="card-header">
        <div class="h4">Exibindo as Moedas</div>
      </div>
      <div class="card-body">
        <HelloWorld :quotes="quotes" />
      </div>

    </div> 
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import api from "@/servidor/api.js";
import {onMounted, reactive, toRefs} from 'vue';

export default {
  name: 'App',
  components: {
    HelloWorld
  },

  //Expor os dados da API no component
  setup() {
    const data = reactive ({ // dados reativos
      quotes: { },
    });

    onMounted( async() => {
      const response = await api.all();
      data.quotes = response.data;
    })

    return { ...toRefs(data) }
  }
}
</script>

<style>
  .h4 {
    text-align: center;
    margin-bottom: 10px;
  }

  .card {
    box-shadow: inset 0 0 1em gold, 0 0 1em red;
  }
</style>
