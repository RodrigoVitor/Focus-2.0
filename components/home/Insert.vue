<template>
  <div class="container">
    <h1 class="text-center mt-4">F O C U S</h1>
    <b-form-input placeholder="Adicionar tarefas" v-model="task"></b-form-input>
    <span v-if="msg !== ''">{{msg}}</span>
    <div class="text-center mt-4">
      <b-button @click="addList" variant="primary" pill>Adicionar</b-button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      task: null,
      msg: ''
    }
  },
  methods: {
    async getTasks () {
      const req = await fetch('http://localhost:3004/tasks')
      const data = await req.json()
      return data
    },
    async addList () {
      // e.preventDefault()

      if (this.task !== null) {
        const data = {
          title: this.task
        }
        const dataJSON = JSON.stringify(data)

        const req = await fetch('http://localhost:3004/tasks', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: dataJSON
        })
        const res = await req.json()
        this.task = null
        this.getTasks()
        location.reload()
        console.log(res)
      } else {
        this.msg = 'Preencha o campo acima'
      }
    }
  }
}
</script>
