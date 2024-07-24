<template>
  <div>
    <h2 class="mr-200">Lista de Clientes</h2>
    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">Nome</th>
          <th scope="col">Idade</th>
          <th scope="col">Cidade</th>
          <th scope="col">Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="cliente in clientes" :key="cliente.id">
          <td>{{ cliente.nome }}</td>
          <td>{{ cliente.idade }}</td>
          <td>{{ cliente.cidade }}</td>
          <td>
            <button class="btn btn-primary" @click="editCliente(cliente)">Editar</button>
            <button class="btn btn-danger" @click="deleteCliente(cliente.id)">Excluir</button>
          </td>
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
    editCliente(cliente) {
      this.$emit('edit-cliente', cliente);
    },
    async deleteCliente(id) {
      try {
        await axios.delete(`http://localhost:8080/cliente/${id}`);
        this.fetchClientes();
      } catch (error) {
        console.error('Erro ao excluir cliente:', error);
      }
    },
  },
};
</script>

<style scoped>
h2 {
  align-items: center;
  text-align: center;
  color: green;
}
.table {
  margin: 20px 80px auto;
  width: 800px auto;
  max-width: 90%;
}
</style>
