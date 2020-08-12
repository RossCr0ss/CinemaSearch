<template>
    <transition name="modal-fade">
        <div class="modal-backdrop">
            <div class="modal">
                <header class="modal-header" id="modalTitle">
                    <slot name="header">
                        This is the default title!
                        <button
                            type="button"
                            class="btn-close"
                            @click="close"
                        >x</button>
                    </slot>
                </header>
                <!-- <section class="modal-body" id="modalDescription">
                    <slot name="body">I'm the default body!</slot>
                </section>-->

                <div class="search">
                    <h1>Search</h1>
                    <input type="text" v-model="query" @keyup="getResult(query)" />
                    <div v-for="result in results" :key="result.id">
                        <p>{{result.title}}</p>
                        <img
                            v-bind:src="'http://image.tmdb.org/t/p/w500/' +    result.poster_path"
                            width="100px"
                        />
                    </div>
                </div>
                <!-- <footer class="modal-footer">
                    <slot name="footer">
                        I'm the default footer!
                        <button
                            type="button"
                            class="btn-green"
                            @click="close"
                        >Close me!</button>
                    </slot>
                </footer>-->
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
                    'https://api.themoviedb.org/3/search/movie?api_key=52c030c67dfc0498ec8a8e7cb063a13b' +
                        query
                )
                .then((response) => {
                    this.results = response.data.results
                })
            console.log(this.results)
        },
    },
}
</script>

<style>
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
    background: #ffffff;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
}

.modal-header,
.modal-footer {
    padding: 15px;
    display: flex;
}

.modal-header {
    border-bottom: 1px solid #eeeeee;
    color: #4aae9b;
    justify-content: space-between;
}

.modal-footer {
    border-top: 1px solid #eeeeee;
    justify-content: flex-end;
}

.modal-body {
    position: relative;
    padding: 20px 10px;
}

.btn-close {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: #4aae9b;
    background: transparent;
}

.btn-green {
    color: white;
    background: #4aae9b;
    border: 1px solid #4aae9b;
    border-radius: 2px;
}
</style>