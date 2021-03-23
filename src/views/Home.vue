<template>
  <div class="home">
    <Header />
    <CarouselShayna />
    <CarouselBannerShayna />
    <InstagramShayna />
    <PartnerShayna />
    <FooterShayna />
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import Header from '@/components/HeaderShayna.vue';
import CarouselShayna from '../components/CarouselShayna.vue';
import CarouselBannerShayna from '../components/CarouselBannerShayna.vue';
import InstagramShayna from '../components/InstagramShayna.vue';
import PartnerShayna from '../components/PartnerShayna.vue';
import FooterShayna from '../components/FooterShayna.vue';

export default {
  name: 'Home',
  components: {
    Header,
    CarouselShayna,
    CarouselBannerShayna,
    InstagramShayna,
    PartnerShayna,
    FooterShayna
  }
}
</script>
