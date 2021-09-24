<template>
  <div>
    <!-- <Navbar /> -->
    <h1 class="mt-5 text-center">G I F T</h1>
    <b-row class="mt-5 border" v-for="gift in gifts" :key="gift.id">
      <b-col>
        <h2 class="text-center">{{ gift.name }}</h2>
      </b-col>
      <b-col>
        <b-button variant="primary">Usado</b-button>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  data () {
    return {
      gifts: []
    }
  },
  methods: {
    async getGift () {
      const req = await fetch('http://localhost:3004/gifts')
      const data = await req.json()
      this.gifts = data
    }
  },
  mounted () {
    this.getGift()
  }
}
</script>

<style scoped>
.border {
  border: 1px solid #000;
  padding:20px 0;
  width:50%;
  margin:auto
}
</style>
