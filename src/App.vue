<template>
    <div id="app">
        <Header />
        <FilmList />
    </div>
</template>

<script>
import Header from '@/components/Header.vue'
import FilmList from '@/components/FilmList.vue'

export default {
    name: 'App',
    components: {
        Header,
        FilmList,
    },
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

*,
*::before,
*::after {
    box-sizing: border-box;
}

ul[class],
ol[class] {
    padding: 0;
}

body,
h1,
h2,
h3,
h4,
p,
ul[class],
ol[class],
li,
figure,
figcaption,
blockquote,
dl,
dd {
    margin: 0;
}

body {
    min-height: 100vh;
    scroll-behavior: smooth;
    text-rendering: optimizeSpeed;
    line-height: 1.5;
}

ul[class],
ol[class] {
    list-style: none;
}

a:not([class]) {
    text-decoration-skip-ink: auto;
}

img {
    max-width: 100%;
    display: block;
}

article > * + * {
    margin-top: 1em;
}

input,
button,
textarea,
select {
    font: inherit;
}

@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
        scroll-behavior: auto !important;
    }
}
</style>
