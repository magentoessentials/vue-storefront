<template>
  <div class="links py10">
    <div class="between-md" v-for="(productLink, index) in products" :key="index">
      <div class="py10" v-if="productLink.product">
        <div class="row middle-xs h4 mb10">
          <p class="col-xs-7 serif m0">{{ productLink.product.name | htmlDecode }}</p>
          <div class="col-xs-4 c-gray">
            <div v-if="productLink.product.special_price && productLink.product.priceInclTax && productLink.product.originalPriceInclTax">
              <span class="price-special">{{ productLink.product.priceInclTax | price }}</span>&nbsp;
              <span class="price-original" >{{ productLink.product.originalPriceInclTax | price }}</span>
            </div>
            <div v-if="!productLink.product.special_price && productLink.product.priceInclTax">
              {{ productLink.product.priceInclTax | price }}
            </div>
          </div>
        </div>

        <div v-if="productLink.product" class="py5">
          <p class="h6 c-gray m0">
            {{ $t('Quantity') }}
          </p>
          <input
            type="number"
            class="product-qty py10 brdr-c-lightgray-secondary bg-transparent h4 weight-300"
            min="1"
            autofocus
            v-model.number="productLink.product.qty"
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { coreComponent } from 'lib/themes'
export default {
  name: 'ProductLinks',
  mixins: [coreComponent('core/ProductLinks')]
}
</script>

<style scoped>
.product-qty {
  border-style: solid;
  border-width: 0 0 1px 0;
  width: 90px;
}
</style>
