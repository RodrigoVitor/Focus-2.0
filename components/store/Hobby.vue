<template>
  <div class="container mt-5">
    <h1 class="text-center"> S T O R E </h1>
    <p v-if="msg !== ''">{{ msg }}</p>
    <b-container class="bv-example-row">
      <b-row>
        <b-col v-for="gift in store" :key="gift.id" cols="6"  class="mt-5 border">
          <h1 class="text-center">{{ gift.name }}</h1>
          <p class="text-center">{{ gift.value }}xp</p>
          <div class="text-center">
            <b-button @click="addGift(gift.name, gift.value)">Comprar</b-button>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  data () {
    return {
      xp: null,
      gift: null,
      msg: '',
      store: [
        { id: 1, name: 'Serie(1)', value: 30 },
        { id: 2, name: 'Filme', value: 50 },
        { id: 3, name: 'Game', value: 30 },
        { id: 4, name: 'Manhã folga', value: 50 },
        { id: 5, name: 'Tarde folga', value: 50 },
        { id: 6, name: 'Noite folga', value: 50 },
        { id: 7, name: '1d folga', value: 150 }
      ]
    }
  },
  methods: {
    async addGift (name, value) {
      if (this.xp >= value) {
        this.gift = name
        this.xp -= value
        const data = {
          name: this.gift
        }
        const dataJSON = JSON.stringify(data)

        const req = await fetch('http://localhost:3004/gifts', {
          method: 'post',
          headers: { 'Content-Type': 'application/json' },
          body: dataJSON
        })
        const res = req.json()
        this.updateXp()
        console.log(res)
        this.msg = name + 'adquirido com sucesso'
        setTimeout(() => { this.msg = '' }, 3000)
        setTimeout(() => location.reload(), 3000)
      } else {
        this.msg = 'Xp insuficiente'
        setTimeout(() => { this.msg = '' }, 3000)
      }
    },
    async getXp () {
      const req = await fetch('http://localhost:3004/myxp')
      const data = await req.json()
      this.xp = data.xp
    },
    async updateXp () {
      const data = {
        xp: this.xp
      }
      const dataJSON = JSON.stringify(data)
      const req = await fetch('http://localhost:3004/myxp', {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: dataJSON
      })
      return req
    }
  },
  mounted () {
    this.getXp()
  }
}
</script>

<style scoped>
.border {
  border: 1px solid #000;
  padding:10px 0;
}
</style>
