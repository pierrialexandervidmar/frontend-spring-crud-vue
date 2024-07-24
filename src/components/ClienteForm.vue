<template>
  <div>
    <h2>{{ isEdit ? 'Editar Cliente' : 'Cadastro de Cliente' }}</h2>
    <form @submit.prevent="submitForm">
      <div>
        <label for="nome">Nome:</label>
        <input type="text" id="nome" v-model="cliente.nome" />
      </div>
      <div>
        <label for="idade">Idade:</label>
        <input type="text" id="idade" v-model="cliente.idade" />
      </div>
      <div>
        <label for="cidade">Cidade:</label>
        <input type="text" id="cidade" v-model="cliente.cidade" />
      </div>
      <button type="submit">{{ isEdit ? 'Salvar' : 'Cadastrar' }}</button>
      <button v-if="isEdit" @click="cancelEdit">Cancelar</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: ['clienteToEdit'],
  data() {
    return {
      cliente: {
        nome: '',
        idade: '',
        cidade: '',
      },
      isEdit: false,
    };
  },
  watch: {
    clienteToEdit(newCliente) {
      if (newCliente) {
        this.cliente = { ...newCliente };
        this.isEdit = true;
      }
    },
  },
  methods: {
    async submitForm() {
      try {
        if (this.isEdit) {
          await axios.put(`http://localhost:8080/cliente/${this.cliente.id}`, this.cliente);
        } else {
          await axios.post('http://localhost:8080/clientes', this.cliente);
        }
        this.$emit('cliente-cadastrado');
        this.resetForm();
      } catch (error) {
        console.error('Erro ao salvar cliente:', error);
      }
    },
    cancelEdit() {
      this.resetForm();
    },
    resetForm() {
      this.cliente = { nome: '', idade: '', cidade: '' };
      this.isEdit = false;
      this.$emit('cancel-edit');
    },
  },
};
</script>
