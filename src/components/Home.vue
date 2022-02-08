<template>
  
  <div>
    <h1 class="display-3 font-weight-light mb-4">Negocie e Colsulte suas ações</h1>
    <v-sheet class="pa-2" color="primary">
      <v-icon class="mr-3">info</v-icon>
      <span>Voce pode Salvar & Carregar Dados</span>
    </v-sheet>
     <v-sheet class="pa-2 mt-3 darken-1" color="success">
      <v-icon class="mr-3">info</v-icon>
      <span>Clique para Oscilar o preço das ações</span>
      
    </v-sheet>
    <v-divider class="mb-4"/>
    <h3><strong>Seu Saldo: {{funds | currency}}</strong></h3>
  </div>
</template>

<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
  },
};
</script>

<style>
</style>
