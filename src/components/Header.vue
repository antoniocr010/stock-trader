<template>
<v-toolbar id="toobar" app>
<v-toolbar-title id="bar" class="headline text-uppercase mr-4">
  <span>Stock</span>
  <span class="font-weight-light">Trader</span>
</v-toolbar-title>
<v-toolbar-items>
  <v-btn flat to="/">Inicio</v-btn>
   <v-btn flat to="/portfolio">Portfolio</v-btn>
    <v-btn flat to="/stocks">Ações</v-btn>
</v-toolbar-items>
<v-spacer/>

<v-toolbar-items>
  <v-btn flat @click="endDay()">Oscilador</v-btn>
 <v-menu offset-y>
   <v-btn flat slot="activator">Salvar & Carregar</v-btn>
   <v-list>
     <v-list-tile @click="saveData()">
       <v-list-tile-title>Salvar Dados</v-list-tile-title>
     </v-list-tile>
      <v-list-tile @click="loadData()">
       <v-list-tile-title >Carregar Dados</v-list-tile-title>
     </v-list-tile>
   </v-list>
 </v-menu>
 <v-layout align-center>
   <span class="text-uppercase grey--text text--darken-2">
   Saldo: {{funds | currency}}
   </span>
 </v-layout>
</v-toolbar-items>
</v-toolbar>
</template>

<script>
import { mapActions } from 'vuex';
export default {
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
  },
  methods: {
    ...mapActions(['randomizeStocks', 'loadData']),
    endDay() {
      this.randomizeStocks();
    },
    saveData() {
      const { funds, stockPortfolio, stocks } = this.$store.getters;
      this.$http.put('data.json', { funds, stockPortfolio, stocks });
    },
    loadDataLocal() {
      this.loadData();
    },
  },
};
</script>

<style scoped>
#toobar {
  border-bottom: 1px solid rgba(78, 79, 78, 0.367);
  justify-content: center;
  align-items: center;
}
#bar {
  border-bottom: 2px solid rgba(19, 164, 19, 0.789);
}
</style>
