<template>
  <div>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
      <div class="container-fluid">
        <div class="row">
          <div class="col-lg-12 mt-5" v-if="products.length > 0">
            <carousel class="product-slider" :items='3' :nav='false' :autoplay='true' :dots='false' >

              <div class="product-item" v-for="product in products" :key="product.id">
                  <div class="pi-pic">
                      <img :src="product.galleries[0].photo" alt="" />
                      <ul>
                          <li class="w-icon active" @click="saveKeranjang(product.id,product.name, product.price, product.galleries[0].photo)">
                              <a href="#"><i class="icon_bag_alt"></i></a>
                          </li>
                          <li class="quick-view">
                              <router-link :to="'/product/' + product.id">
                                  + Quick View
                              </router-link>
                          </li>
                      </ul>
                  </div>
                  <div class="pi-text">
                      <div class="catagory-name">{{ product.type }}</div>
                      <router-link to="/product">
                          <h5>{{ product.name }}</h5>
                      </router-link>
                      <div class="product-price">
                          $ {{ product.price }}
                          <span>$ {{ product.price * 2 }}</span>
                      </div>
                  </div>
              </div>

            </carousel>
          </div>
          <div class="col-lg-12" v-else>
            <p>Produk terbaru belum tersedia untuk saat ini</p>
          </div>
        </div>
      </div>
    </section>
    <!-- Women Banner Section End -->

  </div>
</template>

<script>
import carousel from 'vue-owl-carousel';
import axios from 'axios';

export default {
  name: 'Woman',
  components: {
      carousel,
  },
  data(){
    return {
      products : [],
      keranjangUser : []

    }
  },
  methods: {
    saveKeranjang(id,name,price,photo){
      var productStored = {
        "id" : id,
        "name" : name,
        "price" : price,
        "photo" : photo
      }

      this.keranjangUser.push(productStored)
      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem('keranjangUser', parsed);
    }
  },
  mounted() {
    axios.get('http://127.0.0.1:8000/api/products')
    .then((data) => (this.products = data.data.meta.data.data))
    .catch((err) => console.log(err));
  },
}
</script>

<style scoped>
  .product-item {
  margin-right: 25px;
  }
  .product-item img{
  height: 400px;
  }
</style>