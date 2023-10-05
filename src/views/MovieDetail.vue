<template>
    <div class="movie-detail">
        <img v-if="movie.Poster !== 'N/A'" :src="movie.Poster" alt="poster" />
        <img
            v-else
            src="https://static.vecteezy.com/system/resources/previews/005/337/799/original/icon-image-not-found-free-vector.jpg"
            alt="image not found"
            class="img"
        />
        <div class="detail-text">
            <div>
                <h2>{{ movie.Title }}</h2>
                <p>{{ movie.Year }}</p>
            </div>
            <p>{{ movie.Plot }}</p>
        </div>
    </div>
</template>
<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env";

export default {
    setup() {
        const movie = ref({});
        const route = useRoute();

        onBeforeMount(() => {
            fetch(
                `http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
            )
                .then((res) => res.json())
                .then((data) => {
                    movie.value = data;
                });
        });

        return {
            movie,
        };
    },
};
</script>
<style lang="scss">
.movie-detail {
    max-width: 1000px;
    margin: 40px auto;
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
    padding: 0 10px;
    .detail-text {
        display: flex;
        justify-content: center;
        gap: 20px;
        max-width: 600px;
        flex-wrap: wrap;
        align-items: center;
        text-align: center;
    }
}
</style>
