<template>
  <div class="main">
      <div class="container">
          <div class="content" v-if="contatore > 0">
              <ul v-for="(film, index) in films" :key="`film-${index}`">
                  <li><strong>Titolo:</strong> {{film.title}}</li>
                  <li><strong>Titolo originale:</strong> {{film.original_title}}</li>
                  <li><strong>Lingua:</strong> {{film.original_language}}</li>
                  <li><strong>Voto:</strong> {{film.vote_average}}</li>
              </ul>
          </div>
          <!-- CARICAMENTO IN CASO DI MANCATO CONTENUTO -->
          <div class="loading" v-else>
              <h1>In Attesa di Ricerca...</h1>
              <i class="fas fa-poo-storm"></i>
          </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    name : `Main`,
    props : {
        contatore : Number,
        ricerca : String,
    },
    data() {
        return {
            films : null,
        }
    },
    created() {
        this.prova();
    },
    methods : {
        prova() {

            // Make a request for a user with a given ID
            axios.get('https://api.themoviedb.org/3/search/movie', {
                params: {
                    api_key : `2ed0249aa6ee03db6e9668a23c21f493`,
                    query : this.ricerca,
                    language : `it-IT`,
                }
            })
            .then(response => {
                // handle success
                console.log(response.data.results);
                this.films = response.data.results;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .then(function () {
                // always executed
            });
        }
    }
}
</script>

<style scoped lang="scss">
    .main {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 20px 0;
        .container {
            border: 2px solid grey;
            width: 1200px;
            display: flex;
            align-items: center;
            justify-content: center;
            .loading {
                display: flex;
                justify-content: center;
                flex-direction: column;
                align-items: center;
                padding: 150px 0;
                i {
                    font-size: 40px;
                    animation: colora 4s infinite;
                }
                h1 {
                    animation: colora 4s infinite;
                }
                @keyframes colora {
                    0% {
                        color: white;
                    }
                    50% {
                        color: #e50914;
                    }
                    100% {
                        color: white;
                    }
                }
            }
            .content {
                display: flex;
                flex-wrap: wrap;
                justify-content: center;
                align-items: center;
                ul {
                    padding: 30px;
                }
            }
        }
    }
</style>