<template>
  <div class="home">
    <button @click="showModels">Modelos</button>
    <button @click="showRequirements">Requisitos</button>
    <button @click="showPrices">Precios</button>

    <div v-if="modelsVisible">
      <!-- Aquí puedes personalizar tu grilla de modelos -->
      <Grilla title="Modelos" :rows="modelRows" />
    </div>

    <div v-if="requirementsVisible">
      <!-- Aquí puedes personalizar tu grilla de requisitos -->
      <Grilla title="Requisitos" :rows="requirementRows" />
      <!-- ... -->
    </div>

    <div v-if="pricesVisible">
      <!-- Aquí puedes personalizar tu grilla de precios -->
      <Grilla title="Precios" :rows="priceRows" />
      <!-- ... -->
    </div>
  </div>
</template>

<script>
import Grilla from './components/GrillaTest.vue';
import axios from 'axios';

export default {
  components: {
    Grilla,
  },
  data() {
    return {
      modelsVisible: false,
      requirementsVisible: false,
      pricesVisible: false,
      modelRows: [],
      requirementRows: [
        { name: 'Requisito 1', detail: 'Detalle del requisito 1' },
        { name: 'Requisito 2', detail: 'Detalle del requisito 2' },
        // Agrega más datos de ejemplo aquí
      ],
      priceRows: [
        { name: 'Precio 1', detail: 'Detalle del precio 1' },
        { name: 'Precio 2', detail: 'Detalle del precio 2' },
        // Agrega más datos de ejemplo aquí
      ],
    };
  },
  methods: {
    showModels() {
      this.modelsVisible = true;
      this.requirementsVisible = false;
      this.pricesVisible = false;
    },
    showRequirements() {
      this.modelsVisible = false;
      this.requirementsVisible = true;
      this.pricesVisible = false;
    },
    showPrices() {
      this.modelsVisible = false;
      this.requirementsVisible = false;
      this.pricesVisible = true;
    },
    async fetchModels() {
      const response = await axios.post('https://crm.grupogarden.com.py/group-cars/api/cars/models', 
        { car_code: 1 }, 
        { 
          headers: {
            'Content-Type': 'application/json',
            'accesskey': 'qMCt0NUgrYXRCaThTa2JObTRmZ0pxdENIVmdxQnNaWVE9'
          }
        }
      );

      this.modelRows = response.data.result.map(item => ({
        name: item.model_id,
        detail: item.modelo
      }));
    },
  },
  created() {
    this.fetchModels();
  }
};
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #dae1e1;
}

button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 18px;
  color: white;
  background-color: #039be5;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0277bd;
}

div[data-v-xxxxxxx] {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 10px;
  width: 80%;
  margin: 20px auto;
  padding: 20px;
  background-color: #b2ebf2;
  border-radius: 5px;
}

div[data-v-xxxxxxx] > div {
  padding: 20px;
  background-color: #4dd0e1;
  border-radius: 5px;
  text-align: center;
}
</style>