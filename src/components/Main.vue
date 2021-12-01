<template>
  <div class="main">
      <div class="container">
          <div class="content" v-if="contatore > 0">
              <ul v-for="(film, index) in films" :key="`film-${index}`">
                  <li><img :src="`https://image.tmdb.org/t/p/w185/${film.poster_path}`" alt=""></li>
                  <div class="show">
                    <li><strong>Titolo:</strong> {{film.title}}</li>
                    <li><strong>Titolo originale:</strong> {{film.original_title}}</li>
                    <li v-if="flagResult == false"><strong>Lingua:</strong> {{film.original_language}}</li>
                    <li v-else class="flagStyle"><strong>Lingua:</strong> <img :src="film.original_language" alt=""></li>
                    <li><strong>Voto:</strong> {{film.vote_average}}</li>
                    <li>
                        <i :class = "{star : film.vote_average >= 1}"  class="fas fa-star"></i>
                        <i :class = "{star : film.vote_average >= 2}" class="fas fa-star"></i>
                        <i :class = "{star : film.vote_average >= 3}" class="fas fa-star"></i>
                        <i :class = "{star : film.vote_average >= 4}" class="fas fa-star"></i>
                        <i :class = "{star : film.vote_average >= 5}" class="fas fa-star"></i>
                    </li>
                  </div>
                  <div class="opacity"></div>
              </ul>
              <ul v-for="(serie, index) in series" :key="`serie-${index}`">
                  <li><img :src="`https://image.tmdb.org/t/p/w185/${serie.poster_path}`" alt=""></li>
                  <div class="show">
                    <li><strong>Titolo:</strong> {{serie.title}}</li>
                    <li><strong>Titolo originale:</strong> {{serie.original_title}}</li>
                    <li v-if="flagResult == false"><strong>Lingua:</strong> {{serie.original_language}}</li>
                    <li v-else class="flagStyle"><strong>Lingua:</strong> <img :src="serie.original_language" alt=""></li>
                    <li><strong>Voto:</strong> {{serie.vote_average}}</li>
                  </div>
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
        background-color: #373333;
        .container {
            width: 1200px;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #373333;
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
                    display: flex;
                    flex-direction: column;
                    align-items: center;
                    padding: 0%;
                    margin: 10px;
                    position: relative;
                    border:1px solid white;
                    &:hover .show {
                        display: block;
                    }
                    &:hover .opacity {
                        display: block;
                    }
                    .show {
                        display: flex;
                        position: absolute;
                        color: white;
                        flex-direction: column;
                        align-items: center;
                        display: none;
                        left: 50%;
                        top: 50%;
                        transform: translate(-50%,-50%);
                        z-index: 1;
                        width: 100%;
                        font-size: 13px;
                        .star {
                            color: yellow;
                        }
                    }
                .opacity {
                    width: 100%;
                    height: 100%;
                    position: absolute;
                    top: 0%;
                    left: 0%;
                    background-color: black;
                    opacity: .6;
                    display: none;
                }
                }
            }
        }
    }
</style>