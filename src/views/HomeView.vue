<template>
  <main>
    <ClienteForm @cliente-cadastrado="refreshClientes" />
    <ClienteList ref="clienteList"/>
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
  methods: {
    refreshClientes() {
      this.$refs.clienteList.fetchClientes(); // Chama o método fetchClientes do componente ClienteList para atualizar a lista de clientes
    },
  },
}

</script>

