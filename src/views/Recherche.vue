<template>

    <div class ="recherche">
        <form v-on:submit.prevent="recherche()">

            <div class="input-group">
                <md-field class ="input-group-field">
                    <label> Recherche </label>
                    <md-input v-model="uneRecherche"></md-input>
                </md-field>
               <div class = "input-group-button"><md-button class="md-raised" v-on:click="recherche"><md-icon>search</md-icon></md-button>
                </div>

            </div>
        </form>



    <h2>Résultats de la recherche</h2>

    <md-table>
        <md-table-row v-for="unFilm in films" v-bind:key="unFilm.key">
            <md-table-cell> {{unFilm.title}}</md-table-cell>
            <md-table-cell><img v-bind:src="'http://image.tmdb.org/t/p/w500/'+ unFilm.poster_path" width='100px'> </md-table-cell>

            <md-table-cell> <md-button v-on:click="voirDetails(unFilm)"> <md-icon> visibility</md-icon></md-button></md-table-cell>
           </md-table-row>

    </md-table>
    </div>
</template>


<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';
    import axios from 'axios'

    @Component
    export default class Recherche extends Vue {

        baseUrl = 'https://api.themoviedb.org/3/search/movie';

        films = [];


        uneRecherche = '';

        api_key = '009040dd15ad05cb2bf643f56bc78622';
        movieBackdropSrc='';



        async recherche() {

            const response = await axios.get(this.baseUrl
                + '?api_key=' + this.api_key + '&query=' + this.uneRecherche);
            this.films = await response.data.results;

        }






voirDetails(film:any) {
        this.$router.push({
            path: 'details', query: {
                id: film.id,
                titre: film.title,
                overview:film.overview,
                backdrop_path : film.backdrop_path,

                //release_date:film.release_date,
                //logo_path: film.logo_path,

            }
        });
    }
    }



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }
    ul {
        list-style-type: none;
        padding: 0;
    }
    li {
        display: inline-block;
        margin: 0 10px;
    }
    a {
        color: #42b983;
    }
</style>
