<template>
  <div class="flex justify-center m-6">
    <div v-if="this.product !== null">
      <div class="flex flex-col items-center border rounded-lg bg-gray-100">
        <div class="w-full bg-white rounded-lg flex justify-center">
          <img :src="product.attributes.image.data.attributes.url" width="375" />
        </div>
        <div class="w-full p-5 flex flex-col justify-between">
          <div>
            <h4
              class="
                mt-1
                font-semibold
                text-lg
                leading-tight
                truncate
                text-gray-700
              "
            >
              {{ product.attributes.title }}
            </h4>
            <div class="mt-1 text-gray-600">{{ product.attributes.description }}</div>
          </div>
          <button
            class="
              snipcart-add-item
              mt-4
              bg-white
              border border-gray-200
              d
              hover:shadow-lg
              text-gray-700
              font-semibold
              py-2
              px-4
              rounded
              shadow
            "
            :data-item-id="product.id"
            :data-item-price="product.attributes.price"
            :data-item-description="product.attributes.description"
            :data-item-image="product.attributes.image.data.attributes.url"
            :data-item-name="product.attributes.title"
            v-bind="customFields"
          >
            Add to cart
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: null,
      // storeUrl: process.env.storeUrl,
    };
  },
  created: async function () {
    const res = await fetch(
      `https://lionfish-app-njz74.ondigitalocean.app/api/products/${this.$route.params.productId}?populate=*`
    );
    const response = await res.json();
    this.product = response.data;
    console.log('this.product: ', JSON.stringify(this.product, null, 2));

  },
};
</script>
<style>
</style>
