<template>
  <div>
    <div>
      <p class="float-left"> 0xp </p>
      <b-nav align="center">
        <nuxt-link to="/"> Home </nuxt-link>
        <nuxt-link to="/"> Store </nuxt-link>
        <nuxt-link to="/"> Gift </nuxt-link>
      </b-nav>
    </div>
  </div>
</template>

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
