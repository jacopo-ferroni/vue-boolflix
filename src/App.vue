<template>
  <div id="app">
    <!-- L'HEADER PASSA L'$EMIT ALL'APP.VUE -->
    <Header @filmCercato="ricercaFilmeSerie" @resetFilm="resetListaFilm" />
    <Main :contatore = counter_click :films = films_array :series = series_array :flagResults = flag />
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Main from '@/components/Main.vue'
import Footer from '@/components/Footer.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer,
  },
  data() {
    return {
      counter_click : 0,
      films_array : null,
      series_array : null,
      flag : false,
    }
  },
  methods : {

    ricercaFilmeSerie(search) {
      console.log(search);
      if (search !== ``) {
        this.counter_click = 1;
        axios.get('https://api.themoviedb.org/3/search/movie?', {
          params : {
            api_key : `2ed0249aa6ee03db6e9668a23c21f493`,
            query : search,
            language : `it-IT`,
          }
        })
          .then((response) => {
           /* RICERCA FILM */
          // handle success
          this.films_array = response.data.results
          this.films_array.forEach(element => {
            element.vote_average = Math.floor(element.vote_average / 2);
            /* RICERCA FILM */
            if (element.original_language === `en`) {
              /* Mancano i require */
              element.original_language = `en`;
              element.flag = true;
            }
            else if (element.original_language === `it`) {
              /* mancano i require */
              element.original_language = `it`;
              this.flag = true;
            }
            else {
              this.flag = false;
            }
          });
          })
          .catch(function (error) {
          // handle error
          console.log(error);
          })
          .then(function () {
          // always executed
          });

        /* RICERCA SERIE */
        axios.get('https://api.themoviedb.org/3/search/tv?', {
          params : {
            api_key : `2ed0249aa6ee03db6e9668a23c21f493`,
            query : search,
            language : `it-IT`,
          }
        })
          .then((response) => {
          // handle success
          console.log(response.data.results);
          this.series_array.forEach(element => {
            console.log(element.vote_average);
            console.log(element.original_language);
            if (element.original_language === `en`) {
              /* Mancano i require */
              element.original_language = `en`;
              element.flag = true;
            }
            else if (element.original_language === `it`) {
              /* mancano i require */
              element.original_language = `it`;
              this.flag = true;
            }
            else {
              this.flag = false;
            }
          });
          })
          .catch(function (error) {
          // handle error
          console.log(error);
          })
          .then(function () {
          // always executed
          });
      }
    },

    resetListaFilm(contatoreReset) {
      this.counter_click = contatoreReset;
    }

  }
  
}
</script>

<style lang="scss">
  * {
    margin: 0%;
    padding: 0%;
    box-sizing: border-box;
    font-family: 'Be Vietnam Pro', sans-serif;
    font-family: 'Lato', sans-serif;
  }

  #app {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
</style>