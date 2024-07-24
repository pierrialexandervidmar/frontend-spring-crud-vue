<template>
  <div>
    <div class="navbar navbar-expand-lg navbar-light bg-light mb-4">
      <div class="container-fluid">
        <span class="navbar-brand mb-0 h1">{{ isEdit ? 'Editar Cliente' : 'Cadastro de Cliente' }}</span>
      </div>
    </div>
    <!-- <h2>{{ isEdit ? 'Editar Cliente' : 'Cadastro de Cliente' }}</h2> -->
    <form @submit.prevent="submitForm">
      <img src="@/assets/cliente.png" alt="">
      <div>
        <input type="text" id="nome" v-model="cliente.nome" class="form-control" placeholder="Nome" />
      </div>
      <div>
        <input type="text" id="idade" v-model="cliente.idade" class="form-control" placeholder="Idade" />
      </div>
      <div>
        <input type="text" id="cidade" v-model="cliente.cidade" class="form-control" placeholder="Cidade" />
      </div>
      <button type="submit" class="btn btn-secondary m-2">{{ isEdit ? 'Salvar' : 'Cadastrar' }}</button>
      <button v-if="isEdit" @click="cancelEdit" class="btn btn-warning">Cancelar</button>
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

<style scoped>

img {
  width: 250px;
  margin-bottom: 30px;
}

form {
  width: 500px;
  margin: 30px auto;
  text-align: center;
}

input {
  margin-bottom: 10px;
}

input[type="button"] {
  margin-right: 10px;
}

</style>
