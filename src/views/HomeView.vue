<template>
  <main>
    <ClienteForm 
      @cliente-cadastrado="refreshClientes" 
      @cancel-edit="clearEditCliente" :clienteToEdit="clienteToEdit"
    />
    <ClienteList ref="clienteList" @edit-cliente="editCliente"/>
  </main>
</template>


<script>
import ClienteForm from '../components/ClienteForm.vue';
import ClienteList from '../components/ClienteList.vue';

export default {
  components: {
    ClienteForm,
    ClienteList
  },
  data() {
    return {
      clienteToEdit: null,
    };
  },
  methods: {
    refreshClientes() {
      this.$refs.clienteList.fetchClientes(); // Chama o método fetchClientes do componente ClienteList para atualizar a lista de clientes
    },
    editCliente(cliente) {
      this.clienteToEdit = cliente; // Define o cliente a ser editado
    },
    clearEditCliente() {
      this.clienteToEdit = null;
    },
  },
}

</script>

