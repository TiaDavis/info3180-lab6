<template>
 <div id="articleP">
    <div v-for= "article in articles" class="card" style="width: 18rem;">
        <img class="card-img-top" v-bind:src=article.urlToImage>
        <div class="card-body">
            <h5 class="card-title">{{ article.title }}</h5>
            <p class="card-text">{{article.description}}</p>
        </div>
    </div>
</div>
</template>
<script>
export default {
 data() {
 return {
 articles: []
 };
 },
 created() {
    let self = this;
    fetch('https://newsapi.org/v2/top-headlines?country=us', 
{
    headers: {
    'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
 }
})
    .then(function(response) {
    return response.json();
 })
    .then(function(data) {
    console.log(data);
    self.articles = data.articles;
 });
 }
};
</script>