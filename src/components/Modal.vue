<template>
    <transition name="modal-fade">
        <div class="modal-backdrop">
            <div class="modal">
                <header class="modal__header">
                    <slot name="header">
                        <h1 class="title">Please, write the title of the movie.</h1>
                        <button type="button" class="btn-close" @click="close">x</button>
                    </slot>
                </header>

                <div class="search">
                    <form class="form" @submit.prevent="getResult(query)">
                        <input
                            class="input"
                            type="text"
                            v-model.lazy="query"
                            @keyup.enter.prevent="getResult(query)"
                        />
                    </form>
                    <div class="wrapper">
                        <div class="item" v-for="result in results" :key="result.id">
                            <h3>{{result.title}}</h3>
                            <div class="item__content">
                                <img
                                    v-bind:src="'http://image.tmdb.org/t/p/w500/' + result.poster_path"
                                    class="img"
                                />
                                <ul class="info">
                                    <li class="info__item">
                                        <h3>{{result.title}}</h3>
                                    </li>
                                    <li class="info__item">{{result.release_date}}</li>
                                    <li class="info__item">
                                        <b>{{result.vote_average}}</b>
                                    </li>
                                    <li class="info__item">
                                        <i>{{result.overview}}</i>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Modal',
    data() {
        return {
            showModal: false,
            baseUrl: 'https://api.themoviedb.org/3',
            apiKey: '52c030c67dfc0498ec8a8e7cb063a13b',
            query: '',
            results: '',
        }
    },
    methods: {
        close() {
            this.$emit('close')
        },
        getResult(query) {
            axios
                .get(
                    `${this.baseUrl}/search/movie?api_key=${this.apiKey}&language=en-US&query=${query}&page=1&include_adult=false`
                )
                .then((response) => {
                    this.results = response.data.results
                })
            console.log(this.results)
        },
    },
}
</script>

<style lang="scss">
.modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal {
    background: #fff;
    box-shadow: 2px 2px 20px 1px;
    display: flex;
    flex-direction: column;
    width: 600px;
    padding: 10px 20px;

    &__header {
        border-bottom: 1px solid #eee;
        color: #2b3380;
        display: flex;
        justify-content: center;
        align-items: center;

        .title {
            width: calc(100% - 24px);
        }

        .btn-close {
            border: none;
            font-size: 24px;
            cursor: pointer;
            font-weight: bold;
            background: transparent;
            width: 100%;
            display: flex;
            width: 24px;
            justify-content: center;
            align-items: center;
        }
    }

    .search {
        display: flex;
        flex-direction: column;

        .form {
            margin: 10px 0;

            .input {
                border: none;
                background: #2b3380;
                color: #FFF;
                border-radius: 0.25rem;
                padding: 0.75rem 1rem;
            }
        }

        .wrapper {
            overflow: auto;
            max-height: 600px;

            .item {
                width: 100%;
                display: flex;
                flex-direction: column;
                margin: 5px 0;
                border-radius: 3px;
                padding: 5px 10px;
                border-bottom: 1px solid grey;

                h3 {
                    margin: 10px 0;
                }

                &__content {
                    display: flex;
                    justify-content: flex;

                    .img {
                        background-repeat: no-repeat;
                        background-size: cover;
                        height: 360px;
                        width: 240px;
                    }

                    .info {
                        list-style-type: none;
                        margin-left: 10px;
                        width: calc(100% - 250px);
                        padding: 5px;

                        &__item {
                            margin: 5px 0;
                        }

                        &__item:last-child {
                            text-align: justify;
                        }
                    }
                }
            }
        }
    }
}
</style>