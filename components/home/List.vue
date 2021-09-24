<template>
  <div class="container mt-5">
    <b-card class="mt-4" v-for="task in tasks" :key="task.id">
    <b-row>
      <b-col md="6">
        <p>{{ task.title }}</p>
      </b-col>
      <b-col md="6">
        <b-button variant="primary">Feito</b-button>
        <b-button variant="danger">Não feito</b-button>
      </b-col>
    </b-row>
  </b-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tasks: []
    }
  },
  methods: {
    async getTasks () {
      const req = await fetch('http://localhost:3004/tasks')
      const data = await req.json()
      this.tasks = data
    }
  },
  mounted () {
    this.getTasks()
  }
}
</script>
