<template>

  <section class="bg0 p-t-23 p-b-140">
      <div class="container">
        <div class="p-b-10">
          <h3 class="ltext-103 cl5">
            Product Overview
          </h3>
        </div>
  
        <div class="row isotope-grid">
          <!-- Iterate over each product -->
          <div v-for="product in products" :key="product.id" class="col-sm-6 col-md-4 col-lg-3 p-b-35 isotope-item women">
            <!-- Block2 -->
            <div class="block2">
              <div class="block2-pic hov-img0">
                <!-- Use product thumbnail -->
                <img :src="product.thumbnail" alt="Product Thumbnail">
  
                <a @click="showModal(product)" class="block2-btn flex-c-m stext-103 cl2 size-102 bg0 bor2 hov-btn1 p-lr-15 trans-04">
    Quick View
  </a>
              </div>
  
              <div class="block2-txt flex-w flex-t p-t-14">
                <div class="block2-txt-child1 flex-col-l ">
                  <!-- Product title -->
                  <a :href="'/product-detail/' + product.id" class="stext-104 cl4 hov-cl1 trans-04 js-name-b2 p-b-6">{{ product.title }}</a>
                  <!-- Product price -->
                  <span class="stext-105 cl3">${{ product.price }}</span>
                </div>
  
                <div class="block2-txt-child2 flex-r p-t-3">
                  <!-- Add to wishlist button -->
                  <a href="#" class="btn-addwish-b2 dis-block pos-relative js-addwish-b2">
                    <img class="icon-heart1 dis-block trans-04" src="/images/icons/icon-heart-01.png" alt="ICON">
                    <img class="icon-heart2 dis-block trans-04 ab-t-l" src="/images/icons/icon-heart-02.png" alt="ICON">
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
  
        <!-- Load more -->
        <div class="flex-c-m flex-w w-full p-t-45">
          <a href="#" class="flex-c-m stext-101 cl5 size-103 bg2 bor1 hov-btn1 p-lr-15 trans-04">
            Load More
          </a>
        </div>
      </div>
    </section>
  
  
  
  
  
  <!-- Back to top -->
  <div class="btn-back-to-top" id="myBtn">
      <span class="symbol-btn-back-to-top">
          <i class="zmdi zmdi-chevron-up"></i>
      </span>
  </div>
  
  <!-- Modal1 -->
  <div class="wrap-modal1 js-modal1 p-t-60 p-b-20" v-if="selectedProduct">
      <div class="overlay-modal1 js-hide-modal1"></div>
  
      <div class="container">
        <div class="bg0 p-t-60 p-b-30 p-lr-15-lg how-pos3-parent">
          <button class="how-pos3 hov3 trans-04 js-hide-modal1">
            <img src="/images/icons/icon-close.png" alt="CLOSE">
          </button>
  
          <div class="row">
            <div class="col-md-6 col-lg-7 p-b-30">
              <div class="p-l-25 p-r-30 p-lr-0-lg">
                <div class="wrap-slick3 flex-sb flex-w">
                  <div class="wrap-slick3-dots"></div>
                  <div class="wrap-slick3-arrows flex-sb-m flex-w"></div>
  
                  <div class="slick3 gallery-lb">
                    <!-- Iterate over product images -->
                    <div v-for="(image, index) in selectedProduct.images" :key="index" class="item-slick3" :data-thumb="image">
                      <div class="wrap-pic-w pos-relative">
                        <img :src="image" :alt="'Product Image ' + (index + 1)">
                        <a :href="image" class="flex-c-m size-108 how-pos1 bor0 fs-16 cl10 bg0 hov-btn3 trans-04">
                          <i class="fa fa-expand"></i>
                        </a>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
  
            <div class="col-md-6 col-lg-5 p-b-30">
              <div class="p-r-50 p-t-5 p-lr-0-lg">
                <h4 class="mtext-105 cl2 js-name-detail p-b-14">{{ selectedProduct.title }}</h4>
                <span class="mtext-106 cl2">${{ selectedProduct.price }}</span>
                <p class="stext-102 cl3 p-t-23">{{ selectedProduct.description }}</p>
                <!-- Other details such as size and color selection -->
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        products: [],
        selectedProduct: null
      };
    },
    mounted() {
      // Fetch data from API
      this.fetchData();
    },
    methods: {
      async fetchData() {
        try {
          const response = await fetch('https://dummyjson.com/products');
          const data = await response.json();
          // Assign fetched products to data property
          this.products = data.products;
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      },
      // Show modal and set selected product
      showModal(product) {
        this.selectedProduct = product;
        document.body.classList.add('show-modal1');
      },
      // Hide modal
      hideModal() {
        this.selectedProduct = null;
        document.body.classList.remove('show-modal1');
      }
    }
  }
  </script>