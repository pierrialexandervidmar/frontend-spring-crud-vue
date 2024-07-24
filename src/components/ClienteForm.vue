<template>
  <div>
    <h2>Cadastro de Cliente</h2>
    <form @submit.prevent="submitForm">
      <div>
        <label for="nome">Nome:</label>
        <input type="text" id="nome" v-model="cliente.nome" />
      </div>
      <div>
        <label for="endereco">Idade:</label>
        <input type="text" id="idade" v-model="cliente.idade" />
      </div>
      <div>
        <label for="telefone">Cidade:</label>
        <input type="text" id="Cidade" v-model="cliente.cidade" />
      </div>
      <button type="submit">Cadastrar</button>
    </form>
  </div>
</template>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      cliente: {
        nome: '',
        idade: '',
        cidade: ''
      }
    }
  },
  methods: {
    async submitForm() {
      try {
        await axios.post('http://localhost:8080/cliente', this.cliente);
        this.$emit('cliente-cadastrado');
        this.cliente = { nome: '', idade: '', cidade: '' }; 
      } catch (error) {
        console.error('Erro ao Cadastrar: ', error);
      }
    }
  },
}
</script>