<template>
    <section class="section">
        <div class="container">
            <div class="container">
                <a class="button is-large is-danger">Change My Color</a>
                <p>&nbsp;</p>
            </div>
            <div class="columns is-multiline">
                <div
                    class="column is-one-quarter"
                    v-for="(article, index) in articles"
                    :key="index">
                        <a :href="article.url" target="_blank">
                            <div class="card">
                                <div class="card-image">
                                    <figure class="image is-3by2">
                                        <img :src="article.urlToImage" :alt="article.title">
                                    </figure>
                                </div>
                                <div class="card-content">
                                    <div class="content">{{ article.title }}</div>
                                </div>
                            </div>
                        </a>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
    export default {
        async asyncData({ app }) {
            // register for an api key for free at newsapi.org
            const { articles } = await app.$axios.$get(
                `https://newsapi.org/v2/top-headlines?sources=cnn&apiKey=${
                    process.env.NEWS_API_KEY
                }`
            );

            return { articles };
        },
    };
</script>
<style lang="scss" scoped>
.section {
    // Style resources allow to use variables and functions in vue files
    background: $danger;
}
</style>
