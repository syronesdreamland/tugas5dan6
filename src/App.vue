<template>
  <q-layout view="hHh lpR fFf">
    <!-- Left Drawer -->
    <q-drawer v-model="leftDrawerOpen" side="left" bordered class="bg-grey-1">
      <q-list>
        <q-item-label header>Navigation</q-item-label>
        <q-item clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="home" />
          </q-item-section>
          <q-item-section>
            Home
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="shopping_cart" />
          </q-item-section>
          <q-item-section>
            Cart
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="info" />
          </q-item-section>
          <q-item-section>
            About
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!-- Navbar -->
    <q-header elevated class="bg-primary text-black">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
        <q-toolbar-title>
          Dreamland.id
        </q-toolbar-title>
        <q-btn dense flat round icon="shopping_cart" />
      </q-toolbar>
    </q-header>

    <!-- Main Content -->
    <q-page-container>
      <q-page padding class="q-pa-md">
        
        <!-- Poster Container -->
        <div class="poster-container q-mb-xl">
          <q-img src="poster.jpg" alt="Poster" style="width: 100%; border-radius: 10px;">
            <div class="absolute-bottom text-center text-white" style="width: 100%; padding: 1rem; background: rgba(0, 0, 0, 1); border-radius: 0 0 10px 10px;">
              <div class="text-h4">Promo Spesial Minggu Ini!</div>
              <div class="text-subtitle1">Dapatkan diskon hingga 50% untuk produk pilihan</div>
            </div>
          </q-img>
        </div>

        <!-- Carousel -->
        <q-carousel
          v-model="slide"
          arrows
          infinite
          animated
          control-color="black"
          swipeable
          transition-prev="slide-right"
          transition-next="slide-left"
          height="630px"
          class="bg-dark text-black shadow-2 rounded-borders q-mb-xl"
        >
          <q-carousel-slide v-for="(image, index) in carouselImages" :key="index" :name="index" :img-src="image">
          </q-carousel-slide>
        </q-carousel>

        <!-- Cards -->
        <div style="margin:5px;" class="q-mt-xl row justify-center">
          <q-card v-for="(product, index) in products" :key="product.name" class="my-card q-mb-xl q-pa-md col-l-12 col-sm-12 col-md-12 col-lg-12">
            <q-img :src="product.image" :alt="product.name" class="my-card-img">
              <q-badge color="red" floating>{{ product.discount }} Flash Sale</q-badge>
            </q-img>
            <q-card-section>
              <div class="text-h6 text-center">{{ product.name }}</div>
              <div class="text-subtitle1 text-center">{{ product.price }}</div>
              <!-- * Teks Terjual, Rating, Diskusi, dan Harga Asli * -->
              <div class="text-subtitle2 text-left">Terjual {{ product.sold }}</div>
              <div class="text-subtitle2 text-right">
                <q-icon name="star" color="yellow" /> {{ product.rating }} ({{ product.reviews }} rating)
              </div>
              <div class="text-subtitle2 text-right">Diskusi ({{ product.discussions }})</div><br>
              <div class="text-subtitle2 text-right">
                <del>{{ product.originalPrice }}</del>
                <br>
                <span class="original-price">{{ product.price }}</span>
              </div>
              
              <div class="text-red text-subtitle2 text-right">{{ product.discountPercentage }}% OFF</div>
              <!-- * Pilihan Warna dan Ukuran Pakaian * -->
              <div class="q-mt-md text-center">
                <div class="text-subtitle1">Pilih warna:</div>
                <q-btn-group>
                  <q-btn v-for="color in product.colors" :key="color" :label="color" outline />
                </q-btn-group>
              </div>
              <div class="q-mt-md text-center">
                <div class="text-subtitle1">Pilih ukuran pakaian:</div>
                <q-btn-group>
                  <q-btn v-for="size in product.sizes" :key="size" :label="size" outline />
                </q-btn-group>
              </div>
            </q-card-section>
            <q-card-actions>
              <q-btn flat label="Add to Cart" color="black" />
              <q-btn flat icon="delete" color="red" @click="deleteProduct(index)" />
            </q-card-actions>
          </q-card>
        </div>
      </q-page>
    </q-page-container>

    

    <!-- Footer -->
    <q-footer class="bg-white-8 text-black">
      <q-toolbar>
        <q-toolbar-title class="footer-toolbar">
          &copy; 2022xDreamland
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const slide = ref(0);
    const carouselImages = [
      'image1.jpg',
      'image2.jpg',
      'image3.jpg',
      'image4.jpg'
    ];
    const products = ref([
      { 
        name: 'Samurai Coach Jacket Black - Hitam, M', 
        price: 'Rp185.000', 
        originalPrice: 'Rp470.000', 
        discountPercentage: 61,
        sold: '250+', 
        rating: 4.9, 
        reviews: 282, 
        discussions: 18, 
        image: 'image1.jpg', 
        discount: 'Flash Sale', 
        colors: ['Hitam'], 
        sizes: ['S', 'M', 'L', 'XL']
      },
      // Produk lain bisa ditambahkan di sini
    ]);

    const toggleLeftDrawer = () => {
      leftDrawerOpen.value = !leftDrawerOpen.value;
    };

    const deleteProduct = (index) => {
      products.value.splice(index, 1);
    };

    return {
      leftDrawerOpen,
      toggleLeftDrawer,
      slide,
      carouselImages,
      products,
      deleteProduct
    };
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap');

.custom-card-container > .q-card {
  margin: 10px;
}

.my-card {
  width: 100%;
  max-width: 1400px;
  margin: 0 10px 20px 10px;
  border-radius: 10px;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
}
.my-card-img {
  border-radius: 10px 10px 0 0;
  height: 200px;
}
.text-red {
  color: red;
}
.poster-container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}
.footer-toolbar {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}


</style>
