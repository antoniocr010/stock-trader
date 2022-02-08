<template>
  <v-flex class="pr-3 pb-3" xs12 md6 lg4>
    <v-card class="green darken-3 white--text">
      <strong>{{stock.name}}: <small>{{stock.price | currency}}</small></strong>
    </v-card>
    <v-card>
      <v-container fill-height>
        <v-text-field label="Quantidade" type="number" :error="insufficientFund" v-model.number="quantity"/>
        <v-btn :disabled="insufficientFund || quantity <= 0 || !Number.isInteger(quantity)" class="green darken-3 white--text" @click="buyStock()">
          {{insufficientFund ? 'Sem Fundos': 'Comprar'}}</v-btn>
      </v-container>
    </v-card>
  </v-flex>
</template>

<script>
export default {
  props: ['stock'],
  data() {
    return {
      quantity: 0,
    };
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      };
      this.$store.dispatch('buyStock', order);
      this.quantity = 0;
    },
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    insufficientFund() {
      return this.quantity * this.stock.price > this.funds;
    },
  },
};
</script>

<style>
</style>
