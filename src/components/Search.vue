<template>
  <div class="search-wrapper">
    <h2>{{ title }}</h2>
    <input type="text" v-model="query" @input="filterResults" placeholder="Search something..." />
    <div class="list-wrapper">
      <ul class="list" v-if="!shouldShowWarning">
        <li class="list__item"
          v-for="result in searchResults"
          v-bind:key="result.id">
          <span class="list__item__title">{{ result.title }}</span>
          <span class="list__item__intro">{{ result.body }}</span>
        </li>
      </ul>
      <ul class="list" v-if="shouldShowWarning">
        <li class="list__item">
          <span>No results found :(</span>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  name: 'Search',
  data () {
    return {
      title: 'Search Terms',
      apiKey: 'https://jsonplaceholder.typicode.com/posts?q=lorem',
      query: '',
      apiResults: [],
      searchResults: [],
      shouldShowWarning: false
    }
  },
  methods: {
    getSearchResults () {
      var app = this
      axios.get(this.apiKey).then(function (res) {
        app.apiResults = res.data
      }).catch(function (e) {
        console.log('Error' + e)
      })
    },
    filterResults () {
      const results = this.apiResults.filter(result => {
        return result.title.toLowerCase().startsWith(this.query.toLowerCase())
      })

      this.shouldShowWarning = !this.isQueryEmpty && results.length === 0
      this.searchResults = this.isQueryEmpty ? [] : results
    }
  },
  mounted () {
    this.getSearchResults()
  },
  computed: {
    isQueryEmpty () {
      return this.query.length === 0
    }
  }
}
</script>
