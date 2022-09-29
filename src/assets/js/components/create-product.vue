<template>
  <div id="create-product">
    <form v-on:submit.prevent="addProduct" id="form">
      <div class="form-group">
        <label name="product_peso">WEIGHT</label>
        <input
          type="text"
          name="WEIGHT"
          ref="WEIGHT"
          class="form-control"
          v-model="product.WEIGHT"
          autofocus
          maxlength="12"
          required
        />
      </div>
      <div class="form-group">
        <label name="product_price">NOTA FISCAL</label>
        <input
          type="text"
          name="NOTA_FISCAL"
          ref="NOTA_FISCAL"
          class="form-control"
          v-model="product.NOTA_FISCAL"
          maxlength="12"
        />
      </div>
      <div class="form-group">
        <button class="btn btn-success">Salvar</button>
      </div>
    </form>
  </div>
</template>
<script>
import AllProduct from "./all-products.vue";
import Notification from "./notifications.vue";

export default {
  data() {
    return {
      product: {},
      notifications: [],
      focused: false,
    };
  },
  components: {
    AllProduct,
  },
  methods: {
    created() {
      this.getBooks();
      this.fe();
    },

    addProduct: function () {
      this.$http
        .post("http://10.57.72.121:3012/insertprint", this.product, {
          headers: {
            "Content-Type": "application/json",
          },
        })
        .then((response) => {});
    },
  },
};
</script>
