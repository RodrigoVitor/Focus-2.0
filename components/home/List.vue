<template>
  <div class="container mt-5">
    <b-card class="mt-4" v-for="task in tasks" :key="task.id">
    <b-row>
      <b-col md="6">
        <p>{{ task.title }}</p>
      </b-col>
      <b-col md="6">
        <b-button variant="primary" @click="isDone('true',task.id)">Feito</b-button>
        <b-button variant="danger" @click="isDone('false',task.id)">Não feito</b-button>
      </b-col>
    </b-row>
  </b-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tasks: [],
      xp: null
    }
  },
  methods: {
    async getTasks () {
      const req = await fetch('http://localhost:3004/tasks')
      const data = await req.json()
      this.tasks = data
    },
    async getXp () {
      const req = await fetch('http://localhost:3004/myxp')
      const data = await req.json()
      this.xp = data.xp
    },
    async deleteTask ($id) {
      const req = await fetch('http://localhost:3004/tasks/' + $id, {
        method: 'DELETE'
      })
      const res = await req.json()
      console.log(res)
      location.reload()
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
      const res = req.json()
      console.log(res)
    },
    isDone (done, id) {
      if (done === 'true') {
        this.xp = this.xp + 10
        this.deleteTask(id)
        this.updateXp()
      } else {
        this.xp -= 5
        this.deleteTask(id)
        this.updateXp()
      }
    }
  },
  mounted () {
    this.getTasks()
    this.getXp()
  }
}
</script>
