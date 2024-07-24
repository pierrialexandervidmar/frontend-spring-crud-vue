<template>
  <div>
    <h2>Lista de Clientes</h2>
    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">Nome</th>
          <th scope="col">Idade</th>
          <th scope="col">Cidade</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="cliente in clientes" :key="cliente.id">
          <td>{{ cliente.nome }}</td>
          <td>{{ cliente.idade }}</td>
          <td>{{ cliente.cidade }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      clientes: [],
    };
  },
  async created() {
    this.fetchClientes();
  },
  methods: {
    async fetchClientes() {
      try {
        const response = await axios.get('http://localhost:8080/clientes');
        this.clientes = response.data;
      } catch (error) {
        console.error('Erro ao buscar clientes:', error);
      }
    },
  },
};
</script>

<style scoped>
.table {
  margin-top: 20px;
}
</style>
