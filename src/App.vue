<template>
  <div id="app">
    <!-- L'HEADER PASSA L'$EMIT ALL'APP.VUE -->
    <Header @prova="ricercaFilm"/>
    <Main 
    :contatore = indice_click_ricerca 
    :ricerca = nome_film_da_cercare
    />
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Main from '@/components/Main.vue'
import Footer from '@/components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer,
  },
  data() {
    return {
      indice_click_ricerca : 0,
      nome_film_da_cercare : ``,
    }
  },
  methods : {
    ricercaFilm(search) {
      if(search !== ``) {
        console.log(search);
        this.indice_click_ricerca++;
        this.nome_film_da_cercare = search;
      }
      else {
        this.indice_click_ricerca = 0;
        this.nome_film_da_cercare = ``;
      }
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
}
</style>
