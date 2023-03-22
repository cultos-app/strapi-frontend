<template>
  <div>
    <div class="bg-green-500 p-4 flex justify-between">
      <h1 class="text-white font-bold text-lg">My Awesome Store</h1>
      <button class="text-white font-medium" @click="signOut()">Sign Out</button>
    </div>
    <div
      class="
        m-6
        grid grid-cols-1
        sm:grid-cols-2
        md:grid-cols-2
        lg:grid-cols-2
        xl:grid-cols-2
        gap-4
      "
    >
      <div
        v-for="p in products"
        :key="p.id"
        class="border rounded-lg bg-gray-100 hover:shadow-lg"
      >
        <nuxt-link :to="`/products/${p.id}`">
          <div class="rounded-t-lg bg-white pt-2 pb-2">
            <img class="crop mx-auto" :src="p.attributes.image.data.attributes.url" />
          </div>
          <div class="pl-4 pr-4 pb-4 pt-4 rounded-lg">
            <h4
              class="
                mt-1
                font-semibold
                text-base
                leading-tight
                truncate
                text-gray-700
              "
            >
              {{ p.attributes.title }}
            </h4>
            <div class="mt-1 text-sm text-gray-700">{{ p.attributes.description }}</div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      products: []
    }
  },
  methods: {
    signOut() {
      // Add your signout logic here
    }
  },
  created: async function () {
    const res = await fetch(`https://lionfish-app-njz74.ondigitalocean.app/api/products/?populate=*`)
    const response = await res.json();
    this.products = response.data;
  }
}
</script>
