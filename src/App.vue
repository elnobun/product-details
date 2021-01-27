<template>
  <Suspense>
    <ProductDetails/>
  </Suspense>
</template>

<script>
import ProductDetails from '@/components/ProductDetails'

export default {
  name: 'App',
  components: {
    ProductDetails,
  },
}
</script>
