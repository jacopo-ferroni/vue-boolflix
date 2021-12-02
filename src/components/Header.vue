<template>
  <div class="header">
      <div class="brand">
          <div class="logo">
            <h1>BOOLFLIX</h1>
          </div>
          <a href="#">Home</a>
          <a href="#">Serie TV</a>
          <a href="#">Film</a>
          <a href="#">Nuovi e popolari</a>
          <a href="#">La mia lista</a>
      </div>

      <div class="search">
          <input @keyup.enter="$emit(`filmCercato`, film)" v-model="film" type="text" placeholder="Titoli, persone, generi...">
          <!-- COLLEGAMENTO $EMIT -->
          <div class="button" @click="$emit(`filmCercato`, film)">Cerca</div>
          <div class="button" @click="$emit(`resetFilm`, contatore_reset), delete_space()">Reset</div>
      </div>

      <div class="logIn">
          <div class="button">Iscriviti</div>
          <div class="button">Accedi</div>
      </div>
  </div>
</template>

<script>
export default {
    name : `Header`,
    data() {
        return {
            film : ``,
            contatore_reset : 0,
        }
    },

    created()  {

    },

    methods : {
        delete_space() {
            this.film = ``;
        }
    }
}
</script>

<style scoped lang="scss">
    .header {
        background-color: #373333;
        display: flex;
        align-items: center;
        justify-content: space-between;
        .brand {
            padding: 20px;
            display: flex;
            align-items: center;
            h1 {
                cursor: pointer;
                color: white;
                transition: .5s;
                &:hover {
                    color: #e50914;
                }
            }
            a {
                cursor: pointer;
                text-decoration: none;
                color: white;
                font-size: 10px;
                margin: 0 5px;
                &:hover {
                    color: #e50914;
                }
            }
        }
        .logIn {
            padding: 20px;
            display: flex;
            .button {
                color: white;
                cursor: pointer;
                margin: 0 5px;
                font-size: 10px;
                &:hover {
                    color: #e50914;
                }
            }
        }
        .search {
            display: flex;
            align-items: center;
            input {
                padding: 10px;
                width: 300px;
                border: .5px solid white;
                background-color: black;
            }
            input[placeholder] {
                color: white;
            }
            .button {
                color: white;
                border: 2px solid wjite;
                border-radius: 20px;
                margin-left: 10px;
                cursor: pointer;
                font-size: 10px;
                &:hover {
                    color: #e50914;
                }
            }
        }
    }

</style>