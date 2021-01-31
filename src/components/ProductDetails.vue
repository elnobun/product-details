<template>
  <div class="product">

    <!--  Product Title  -->
    <div class="product__title">
        <h1 class="align">{{ product.title }}</h1>
    </div>

    <!-- Contributor Author -->
    <div class="product__author-name align" v-for="author in product.contributors" :key="author.name">
        <p>By {{ author.contributor.name }}</p>
    </div>

    <!--  Author Bio  -->
    <div class="product__about-bio paper" v-for="author in product.contributors" :key="author.name">
      <h4 class="header__caption">About The Author</h4>
      <span v-html="author.contributor.bio"></span>
    </div>

    <!--  Product Image  -->
    <div class="product__image">
      <img class="paper" :src="formatData(product.image, /x145/g, 'x400' )" alt="book image">
    </div>

    <!-- Product Description -->
    <div class="product__description paper">
      <h4 class="header__caption">Product Description</h4>
      <span v-html="formatData(product.description, /&nbsp/g, '')"></span>
    </div>


    <!--  Product Prices -->
    <div class="product__prices align">
      <sub class="price_tag">Prices</sub>
      <div class="price__amount">
        <div v-for="(price, index) in product.prices" :key="index">
          <p>{{ price.locale }} {{ price.amount }}</p>
        </div>
      </div>
    </div>


    <!-- Product Sale Date -->
    <div class="product__sale align">
      <span class="sale__date">Sale Date:</span>
      <span> March 15, {{ formatData(product.sale_date.date, /-03-15 00:00:00.000000/, "")}}</span>
    </div>


    <!-- Product Reviews -->
    <div class="product__reviews paper">
      <h4 class="header__caption">Reviews</h4>
      <div class="reviews" v-for="reviews in product.reviews" :key="reviews.review_id">
        <q>{{formatData(reviews.review.description, /[“”]/g, "" )}}</q>
        <p v-html="reviews.review.reviewer"></p>
      </div>
    </div>

    <!-- Product Retailer Links -->
    <div class="product__retailers">
      <h4 class="header__caption">Retailer Links</h4>
      <div class="retail__links">
        <ul v-for="retailer in product.retailers" :key="retailer.path">
          <li class="btn">
            <a :href="retailer.path" target="_blank" rel="noreferrer">{{ retailer.label }}</a>
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

  // VueJS3 composition API, doing asynchronous job under the hood.
  async setup () {
    // Return product default state
    const product = ref(null)

    // Fetch JSON data
    const productResponse = await fetch('https://v3-static.supadu.io/dev/products/9780060577315.json')
    // Set product value to JSON response
    product.value = await productResponse.json()

    // Function to format HTML data
    function formatData(data, str, replace) {
      return data.replace(str, replace)
    }

    // Return data object, so that it becomes available to use in the template
    return {
      product,
      formatData
    }
  },
}
</script>
