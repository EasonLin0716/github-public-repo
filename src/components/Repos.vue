<template>
  <div id="repos" class="container">
    <h1 class="mb-4">My github repos</h1>
    <div v-for="repo in repos" :key="repo.id" class="card mb-4">
      <div class="card-body">
        <h5 class="card-title">{{ repo.name }}</h5>
        <p class="card-text">
          {{
            repo.description ? repo.description : 'no description in this repo'
          }}
        </p>
        <a :href="repo.html_url" class="card-link">Link to the repo</a>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'

export default {
  name: 'Repos',
  data() {
    return {
      repos: []
    }
  },
  methods: {
    async fetchData(num, page) {
      try {
        const { data } = await axios.get(
          `https://api.github.com/users/EasonLin0716/repos?per_page=${num}&page=${page}`
        )
        if (!data.length) return
        data.forEach(repo => this.repos.push(repo))
      } catch (error) {
        throw new Error()
      }
    }
  },
  created() {
    const loadDataNum = Math.floor(window.screen.height / 140)
    let page = 2
    const self = this
    self.fetchData(loadDataNum, 1)
    document.addEventListener('scroll', function() {
      if (window.scrollY + 1000 > document.body.offsetHeight) {
        self.fetchData(loadDataNum, page)
        page += 1
      }
    })
  }
}
</script>
