<template>
  <v-flex class="pr-3 pb-3" xs12 md6 lg4>
    <v-card class="blue darken-3 white--text">
      <strong>{{stock.name}}: <small>{{stock.price | currency}} Qtde: {{stock.quantity}}</small></strong>
    </v-card>
    <v-card>
      <v-container fill-height>
        <v-text-field label="Quantidade" type="number" :error="insufficientQuant" v-model.number="quantity"/>
        <v-btn :disabled="insufficientQuant || quantity <= 0 || !Number.isInteger(quantity)"
         class="blue darken-3 white--text" @click="sellStock()">{{insufficientQuant ? 'Sem Fundos': 'Vender'}}</v-btn>
      </v-container>
    </v-card>
  </v-flex>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  props: ['stock'],
  data() {
    return {
      quantity: 0,
    };
  },
  computed: {
    insufficientQuant() {
      return this.quantity > this.stock.quantity;
    },
  },

  methods: {
    ...mapActions({ sellStockAction: 'sellStock' }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      };

      this.sellStockAction(order);
      // this.$store.dispatch('sellStock', order);
      this.quantity = 0;
    },
  },
};
</script>

<style>
</style>
