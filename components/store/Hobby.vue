<template>
  <div class="container mt-5">
    <h1 class="text-center">S T O R E</h1>
    <b-container class="bv-example-row">
      <b-row>
        <b-col cols="6" class="mt-5 border" v-for="gift in store" :key="gift.id">
          <h1 class="text-center">{{ gift.name }}</h1>
          <p class="text-center">{{ gift.value }}xp</p>
          <div class="text-center">
            <b-button>Comprar</b-button>
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
      store: [
        { id: 1, name: 'Serie(1)', value: 35 },
        { id: 2, name: 'Filme', value: 50 },
        { id: 3, name: 'Brasfoot', value: 30 },
        { id: 4, name: 'Manhã folga', value: 50 },
        { id: 5, name: 'Tarde folga', value: 50 },
        { id: 6, name: 'Noite folga', value: 50 },
        { id: 7, name: '1d folga', value: 150 }
      ]
    }
  }
}
</script>

<style scoped>
.border {
  border: 1px solid #000;
  padding:10px 0;
}
</style>
