<template>
  <div>
    <div>
      <p class="float-left"> {{ xp }}xp </p>
      <b-nav align="center">
        <nuxt-link to="/"> Home </nuxt-link>
        <nuxt-link to="/store"> Store </nuxt-link>
        <nuxt-link to="/gift"> Gift </nuxt-link>
      </b-nav>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      xp: null
    }
  },
  methods: {
    async getXp () {
      const req = await fetch('http://localhost:3004/myxp')
      const data = await req.json()
      this.xp = data.xp
    }
  },
  mounted () {
    this.getXp()
  }
}
</script>

<style scoped>
div {
 padding:5px;
}

div div {
    background-color:blue;
    color:white
}
p {
    font-size:1.2rem;
}
a{
    color:white;
    margin-left:10px
}
a:hover {
    color:gray
}
</style>
