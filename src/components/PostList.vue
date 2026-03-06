<template>
    <div class="list">
        <a v-for="post in filteredPosts" :key="post.id" :href="post.url">
            <img :src="post.images.image460.webpUrl" :alt="post.title" />
            <h2>{{ post.title }}</h2>
            <span class="datetime">{{ formatDate(post.creationTs) }}</span>
        </a>
    </div>
</template>

<script>
export default {
    props: ['filter'],
    data() {
        return {
            posts: []
        }
    },
    computed: {
        filteredPosts() {
            return this.posts.filter(post => {
                return post.title.toLowerCase().includes(this.filter.toLowerCase()) ||
                    post.description.toLowerCase().includes(this.filter.toLowerCase()) ||
                    new Date(post.creationTs * 1000).toLocaleDateString('sk-SK').includes(this.filter) ||
                    post.tags.some(tag => tag.key.toLowerCase().includes(this.filter.toLowerCase()))
            })
        }
    },
    methods: {
        formatDate(timestamp) {
            return new Date(timestamp * 1000).toLocaleDateString('sk-SK')
        }
    },
    async mounted() {
        const response = await fetch(process.env.BASE_URL + 'output.json')
        this.posts = await response.json()
    }
}
</script>

<style scoped>
a { 
    display: block;
    text-decoration: none;
    padding: 1em;
    border: 1px solid #ddd;
    background-color: #fff;
    color: #000
}
h2 {
    font-size: 1em;
    margin: 0.5em 0 0.5em;
}
img {
    object-fit: contain;
    max-width: 100%;
}
.list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1em;
    grid-template-rows: masonry;
}
.datetime {
    color: #999;
    font-size: 0.8em;
}
</style>