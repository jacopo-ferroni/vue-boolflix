<template>
  <div class="main">
      <div class="container">
          <div class="content" v-if="contatore > 0">
              <ul v-for="(film, index) in films" :key="`film-${index}`">
                  <li><img :src="`https://image.tmdb.org/t/p/w92/${film.poster_path}`" alt=""></li>
                  <li><strong>Titolo:</strong> {{film.title}}</li>
                  <li><strong>Titolo originale:</strong> {{film.original_title}}</li>
                  <li v-if="flagResult == false"><strong>Lingua:</strong> {{film.original_language}}</li>
                  <li v-else class="flagStyle"><strong>Lingua:</strong> <img :src="film.original_language" alt=""></li>
                  <li><strong>Voto:</strong> {{film.vote_average}}</li>
              </ul>
              <ul v-for="(serie, index) in series" :key="`film-${index}`">
                  <li><img :src="`https://image.tmdb.org/t/p/w92/${serie.poster_path}`" alt=""></li>
                  <li><strong>Titolo:</strong> {{serie.title}}</li>
                  <li><strong>Titolo originale:</strong> {{serie.original_title}}</li>
                  <li v-if="flagResult == false"><strong>Lingua:</strong> {{serie.original_language}}</li>
                  <li v-else class="flagStyle"><strong>Lingua:</strong> <img :src="serie.original_language" alt=""></li>
                  <li><strong>Voto:</strong> {{serie.vote_average}}</li>
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

export default {
    name : `Main`,
    props : {
        films : Array,
        series : Array,
        contatore : Number,
        flagResult : Boolean,
    },
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
                    list-style: none;
                }
            }
        }
    }
</style>