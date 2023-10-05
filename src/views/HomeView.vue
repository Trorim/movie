<template>
    <div class="home">
        <div class="feature-card">
            <router-link to="/movie/tt0409591">
                <img
                    class="feature-img"
                    src="https://w.forfun.com/fetch/6f/6feb85f23b24f2e9ed6e75069f065fdb.jpeg"
                    alt="Naruto"
                />
                <div class="detail">
                    <h3>Naruto</h3>
                    <p>
                        Many years ago, in the hidden village of Konoha, lived a
                        great demon fox. When it swung one of it's nine tails, a
                        tsunami occurred. The fourth hokage sealed this demon
                        fox inside a boy in exchange for his own life. Naruto
                        was that boy, and he grew up with no family, and the
                        villagers hated him thinking that he himself was the
                        demon fox. Naruto's dream is to become Hokage, and have
                        the villagers acknowledge him.
                    </p>
                </div>
            </router-link>
        </div>
        <div class="container">
            <form @submit.prevent="SearchMovies()" class="search-box">
                <input
                    type="text"
                    class="search-input"
                    placeholder="What are you looking for?"
                    v-model="search"
                />
                <button type="submit" class="search-btn">Search</button>
            </form>
            <div class="movie-list">
                <div class="movie" v-for="movie in movies" :key="movie.imdbID">
                    <router-link
                        :to="'/movie/' + movie.imdbID"
                        class="movie-link"
                    >
                        <div class="product-image">
                            <img
                                class="img"
                                v-if="movie.Poster !== 'N/A'"
                                :src="movie.Poster"
                                alt="movie poster"
                            />
                            <img
                                v-else
                                class="img"
                                src="https://static.vecteezy.com/system/resources/previews/005/337/799/original/icon-image-not-found-free-vector.jpg"
                                alt="image not found"
                            />
                            <div class="type">{{ movie.Type }}</div>
                        </div>
                        <div class="desrc">
                            <p class="year">{{ movie.Year }}</p>
                            <h3>{{ movie.Title }}</h3>
                        </div>
                    </router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";

export default {
    setup() {
        const search = ref("");
        const movies = ref([]);

        const SearchMovies = () => {
            if (search.value !== "") {
                try {
                    fetch(
                        `http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`
                    )
                        .then((res) => res.json())
                        .then((data) => {
                            movies.value = data.Search;
                            search.value = "";
                        });
                } catch (error) {
                    alert("Произошла ошибка!");
                }
            }
        };

        return {
            search,
            movies,
            SearchMovies,
        };
    },
};
</script>

<style>
.img {
    width: 300px;
    height: 480px;
    object-fit: cover;
}

.feature-card {
    position: relative;
}

.feature-img {
    position: relative;
    display: block;
    width: 100%;
    height: 300px;
    object-fit: cover;
    object-position: center 65%;
}
.detail {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.6);
    width: 100%;
    height: 120px;
    padding: 20px;
    color: #fff;
    overflow: hidden;
    h3 {
        margin-bottom: 15px;
    }
}
.search-box {
    display: flex;
    flex-direction: column;
    gap: 10px;
    justify-content: center;
    align-items: center;
    margin: 20px auto;
    min-width: 300px;
    .search-input {
        width: 80%;
        height: 30px;
        border-radius: 20px;
        border: none;
        padding: 20px;
        transition: all 0.3s;
        &:focus {
            outline: none;
            box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.6);
        }
    }
    .search-btn {
        width: 150px;
        height: 30px;
        border-radius: 20px;
        border: none;
        box-shadow: 0px 2px 2px grey;
        transition: all 0.3s;
        background-color: azure;
        &:active {
            transform: translateY(2px);
            box-shadow: none;
        }
    }
}

.movie-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, auto));
    gap: 20px;
    justify-content: center;
    padding: 0 10px;
    .type {
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        bottom: 11px;
        left: 8px;
        width: 100px;
        height: 30px;
        background-color: bisque;
        text-transform: uppercase;
    }
    .desrc {
        background-color: grey;
        padding: 10px;
        border-radius: 0px 0px 10px 10px;
        text-transform: capitalize;
        width: 100%;
    }
}

.movie {
    width: 300px;
    /* height: 600px; */
}

.product-image {
    position: relative;
    display: flex;
    img {
        display: block;
        width: 100%;
        height: 275px;
        object-fit: cover;
    }
}
</style>
