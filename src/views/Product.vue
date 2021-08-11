<template>
  <div class="product">
    <Header />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more">
                        <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="gambar_default" alt="" style="width:1024px;"/>
                            </div>
                            <div class="product-thumbs" v-if="productDetail.galleries.length > 0">
                                <carousel class="product-thumbs-track ps-slider" :dots="false" :nav="false">
                                    <div 
                                    v-for="ss in productDetail.galleries"
                                    :key="ss.id"
                                    class="pt" @click="ChangeImage(ss.photo)" 
                                    :class="ss.photo==gambar_default ? 'active' : ''">
                                        <img :src="ss.photo" alt="" />
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{productDetail.type}}</span>
                                    <h3>{{productDetail.name}}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p>
                                        {{productDetail.description}}
                                    </p>
                                    <h4>${{productDetail.price}}</h4>
                                </div>
                                <div class="quantity item-center">
                                   <router-link to="/cart" class="primary-btn pd-cart">Add To Cart</router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedProductShayna/>
    <FooterShayna />
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import Header from '@/components/HeaderShayna.vue';
import RelatedProductShayna from '@/components/RelatedProductShayna.vue';
import FooterShayna from '../components/FooterShayna.vue';
import carousel from 'vue-owl-carousel';
import axios from 'axios';

export default {
  name: 'product',
  components: {
    Header,
    RelatedProductShayna,
    FooterShayna,
    carousel
  },
  data(){
      return{
          gambar_default:"",
          thumbs:[
              "img/mickey1.jpg",
              "img/mickey2.jpg",
              "img/mickey3.jpg",
              "img/mickey4.jpg"
          ],
          productDetail : []
      }
  },
  methods:{
    ChangeImage(urlImage){
          this.gambar_default = urlImage;
    },
    setDataPicture(data){
      //replace object productDetail dengan data dari API
      this.productDetail = data
      //replace value gambar default dengan data dari API (galleries)
      this.gambar_default = data.galleries[0].photo;
    }
  },

  mounted(){
      axios
        .get("http://127.0.0.1:8000/api/products", {
            params : {
                id: this.$route.params.id
            }
        })
        .then(res => (this.setDataPicture(res.data.data)))

        .catch(err => console.log(err));
  }
}
</script>

<style scoped>
.pt{
    margin-right: 5px;
}
</style>
