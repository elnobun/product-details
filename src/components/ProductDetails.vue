<template>
  <div class="product">

    <!--  Product Image  -->
    <div class="product__image">
      <img class="paper" :src="product.image" alt="book image">
    </div>

    <!--  Product Title  -->
    <div class="product__title">
      <h1>{{ product.title }}</h1>
      <!-- Contributor Name and Bio -->
      <div class="product__author-name" v-for="author in product.contributors" :key="author.name">
        <p>By <span>{{ author.contributor.name }}</span></p>
      </div>
    </div>

<!--    <hr class="line">-->

    <!--  Product Prices -->
    <div class="product__prices">
      <sub class="price_tag">Prices</sub>
      <div class="price__amount">
        <div v-for="(price, index) in product.prices" :key="index">
          <p>{{ price.locale }} {{ price.amount }}</p>
        </div>
      </div>
    </div>


    <!-- Product Sale Date -->
    <div class="product__sale">
      <span class="sale__date">Sale Date:</span>
      <span> March 15, {{ product.sale_date.date.replace(/-03-15 00:00:00.000000/, '') }}</span>
    </div>

    <!--  Author Bio  -->
    <div class="product__about-bio paper" v-for="author in product.contributors" :key="author.name">
      <h4 class="header__caption">About The Author</h4>
      <span v-html="author.contributor.bio"></span>
    </div>

    <!-- Product Description -->
    <div class="product__description paper">
      <h4 class="header__caption">Product Description</h4>
      <span v-html="product.description.replace(/&nbsp/g, '')"></span>
    </div>

    <!-- Product Reviews -->
    <div class="product__reviews paper">
      <h4 class="header__caption">Reviews</h4>
      <div class="reviews" v-for="reviews in product.reviews" :key="reviews.review_id">
        <q>{{ reviews.review.description.replace(/[“”]/g, '') }}</q>
        <p v-html="reviews.review.reviewer"></p>
      </div>
    </div>

    <!-- Product Retailer Links -->
    <div class="product__retailers">
      <h4 class="header__caption">Retailer Links</h4>
      <div class="retail__links">
        <ul v-for="retailer in product.retailers" :key="retailer.path">
          <li class="btn">
            <a :href="retailer.path" target="_blank">{{ retailer.label }}</a>
          </li>
        </ul>
      </div>
    </div>

  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'ProductDetails',

  async setup () {
    const product = ref(null)

    const productResponse = await fetch('https://v3-static.supadu.io/dev/products/9780060577315.json')
    product.value = await productResponse.json()

    return {
      product,
    }
  },
}
</script>
