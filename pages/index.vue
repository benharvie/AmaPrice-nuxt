<template>
  <div class="flex h-screen">
    <div class="m-auto d-flex">
      <p>eg. B00J5ERXZM</p>
      <div class="flex rounded-full border-grey-light border">
        <button>
          <span class="w-auto flex justify-end items-center text-grey p-2">
            <i class="material-icons text-3xl"></i>
          </span>
        </button>
        <input
          class="w-full rounded mr-4"
          type="text"
          v-model="asin"
          placeholder="Search by ASIN..."
          @keypress.enter="getPrices()"
        />
      </div>
      <table class="table-auto" v-if="priceList">
        <thead>
          <tr>
            <th>Domain</th>
            <th>Price</th>
            <th>Buy Now</th>
          </tr>
        </thead>
        <tbody>
          <tr
            :key="price.domain"
            v-for="price in priceList"
            :class="price.price ? '' : 'bg-red-400'"
          >
            <th>{{ price.domain }}</th>
            <th>{{ price.price ? price.price : 'N/A' }}</th>
            <th>Buy Now</th>
          </tr>
        </tbody>
      </table>
      <!-- <div v-if="priceList">
        <ul>
          <li :key="price.domain" v-for="price in priceList">
            ~ {{ price.domain }} | {{ price.price ? price.price : 'N/A' }}
          </li>
        </ul>
      </div> -->
    </div>
  </div>
</template>

<style></style>

<script>
const domains = [
  // [ EUROPE ]
  '.co.uk',
  '.fr',
  '.it',
  '.es',
  '.de',
  '.nl'

  // [ WORLDWIDE ]
  // ".com",
  // ".ca",
  // ".cn",
  // ".in",
  // ".co.jp",
  // ".sg",
  // ".com.tr",
  // ".com.mx",
  // ".com.au",
  // ".com.br",
]
export default {
  data() {
    return {
      asin: '',
      priceList: ''
    }
  },
  methods: {
    // B00J5ERXZM
    async getPrices() {
      await fetch(`http://localhost:3333/search/${this.asin}`)
        .then(response => response.json())
        .then(jsonResponse => {
          this.priceList = jsonResponse.priceList
        })
    }
  }
}
</script>
