<template>
    <div class="film_list">
        <h1 class="title">Popular movies</h1>
        <div class="wrapper">
            <article class="item shadow" v-for="item in results" :key="item.id">
                <!-- :style="{ backgroundImage: `url(http://image.tmdb.org/t/p/w500/${item.poster_path})` }" -->
                <img
                    class="img"
                    :src="`http://image.tmdb.org/t/p/w500/${item.poster_path}`"
                    alt="no-image"
                />
                <div class="info">
                    <h4 class="title">{{item.title}}</h4>
                    <p class="date">{{item.release_date}}</p>
                </div>
            </article>
        </div>
        <div class="more" :class="{'is-hidden' : currentPage == totalPages}">
            <button @click="loadMore" class="button">Load More</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'FilmList',
    components: {
        
    },
    data() {
        return {
            results: [],
            baseUrl: 'https://api.themoviedb.org/3',
            apiKey: '52c030c67dfc0498ec8a8e7cb063a13b',
            currentPage: 1,
            totalPages: 500,
        }
    },
    computed: {
        request() {
            return `${this.baseUrl}/movie/popular?api_key=${this.apiKey}&language=en-US&page=${this.currentPage}`
        },
    },
    created() {
        this.fetchFilms()
    },
    methods: {
        fetchFilms() {
            axios.get(this.request).then((response) => {
                this.results = response.data.results
                console.log(this.results)
            })
        },
        loadMore() {
            this.currentPage++
            this.fetchFilms()
        },
    },
}
</script>

<style lang="scss">
.film_list {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 60%;
    margin: 0 auto 20px;

    .title {
        margin: 20px 0;
    }

    .wrapper {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        margin-bottom: 20px;

        .shadow {
            -webkit-box-shadow: 3px 3px 5px 6px #ccc;
            -moz-box-shadow: 3px 3px 5px 6px #ccc;
            box-shadow: 3px 3px 5px 6px #ccc;
        }

        .item {
            width: 240px;
            margin: 5px;
            display: flex;
            flex-direction: column;
            justify-content: flex-start;

            img {
                background-repeat: no-repeat;
                background-size: cover;
                height: 360px;
            }

            .info {
                margin: 5px 0;
                padding: 5px 20px;
                min-height: 100px;
                display: flex;
                flex-direction: column;
                align-items: flex-start;
                text-align: start;

                .title,
                .date {
                    margin: 5px 0;
                }
            }
        }
    }
}

.film_list .button-more {
    margin: 10px 0;
}

.button {
    width: 120px;
    padding: 10px;
    border-radius: 5px;
    background-color: #2b3380;
    color: #fff;
}

.button:hover {
    background-color: #fff;
    color: #2b3380;
    cursor: pointer;
}
</style>