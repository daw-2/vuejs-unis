<template>
  <div>
    <div class="row">
      <div class="col-4" v-for="product in products" :key="product.id">
        <div class="card mb-5">
          <div class="card-body">
            <h4 class="card-title">
              <router-link :to="'/products/'+product.id">
                {{ product.name }}
              </router-link>
            </h4>

            <button @click="addProductToCart(product)"
                    class="btn btn-primary">
              Ajouter au panier
            </button>

            <router-link class="btn btn-info"
              :to="'/products/edit/'+product.id"
            >
              Modifier
            </router-link>
            <router-link class="btn btn-danger"
              :to="'/products/delete/'+product.id"
            >
              Supprimer
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  data () {
    return {
      products: []
    }
  },
  methods: {
    ...mapActions(['addProductToCart'])
  },
  mounted () {
    this.$http.get('http://localhost:3000/products').then(response => {
      this.products = response.data
    })
  }
}
</script>
