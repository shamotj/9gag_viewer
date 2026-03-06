<template>
  <FilterPosts @filter-changed="updateFilter" />
  <PostList :filter="filter" />
</template>

<script>
import FilterPosts from './components/FilterPosts.vue'
import PostList from './components/PostList.vue'

export default {
  name: 'App',
  components: {
    FilterPosts,
    PostList
  },
  data() {
    return {
      filter: ''
    }
  },
  methods: {
    updateFilter(filter) {
      this.filter = filter
    }
  }
}
</script>

<style>
body {
  background-color: #eee;
}
#app {
  font-family: Droid Sans, sans-serif;
  text-align: center;
}
</style>
