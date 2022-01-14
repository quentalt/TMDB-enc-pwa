<template>
    <div class="details">
        <h1> Details du film</h1>
        <div class="content">
            <md-card class ="details-card">
                <md-steppers md-alternative >
                <md-step>

                           <md-table>{{film.titre}}</md-table>
                            <md-table>  {{film.id}}</md-table>
            <md-table>
                <md-table-row v-for="unGenre in genre" v-bind:key="unGenre.key">
                        <md-table-cell>{{unGenre.name}}</md-table-cell>
                    </md-table-row>
            </md-table>
                </md-step>
                    <md-step>
                        <md-card>
                            <md-card-media alt="image devant"><img v-bind:src="'http://image.tmdb.org/t/p/original/'+ film.poster_path"> </md-card-media>
                            <md-card-media alt="image arriere"><img v-bind:src="'http://image.tmdb.org/t/p/w150_and_h225_bestv2/'+ film.backdrop_path"> </md-card-media>

                        </md-card>

                    </md-step>
                </md-steppers>

            </md-card>

        </div>
        </div>
</template>

<script lang="ts">
    import {Component,Vue} from 'vue-property-decorator';
    import axios from "axios";


    export default class Details extends Vue {
        genresUrl = 'https://api.themoviedb.org/3/movie/';
        film: any;
        api_key = '009040dd15ad05cb2bf643f56bc78622';
        genre=[];
        uneRecherche = '';



        created() {


            this.film = {

                id: this.$route.query.id,
                titre: this.$route.query.titre,
            }
            this.rechercheGenres();

        }

        async rechercheGenres() {

            axios.get(this.genresUrl+ this.film.id+ '?api_key=' + this.api_key).then(async response => {
                this.genre = await response.data.genres;
                console.log(this.genre);
            })
                .catch((error: any) => {
                    console.log(error)
                })
        };
        }









































        /*getMoviesByGenre() { // To filter movies by selected genre
            this.page = 1; // Show filtered results stating at page one
            if (this.genreSelected !== "all") {
                this.filteredMovies = this.film.filter((films: { genre: { name: string | string[]; }; }) => {
                    return films.genre.name.indexOf(this.genreSelected) > -1;*/











</script>

<style scoped>

</style>
